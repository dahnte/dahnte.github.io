<script lang="ts">
    import { onMount } from 'svelte';
    let lat: string, long: string, acc: string;
    let streaming:boolean = false;
    let isFacingModeUser:boolean = true;
    
    const geoOptions = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0,
    };
    
    function geoSuccess(pos) {
        lat = pos.coords.latitude;
        long = pos.coords.longitude;
        acc = pos.coords.accuracy;
    }
    
    function geoError(err) {
        console.warn(`ERROR(${err.code}): ${err.message}`);
    }
    
    function findLoc() {
        navigator.geolocation.getCurrentPosition(geoSuccess, geoError, geoOptions);
        document.getElementById('geo-detail')!.hidden = false;
    }
    
    // Fill the photo with an indication that none has been
    // captured.
    function clearPhoto() {
        const context = canvas.getContext("2d");
        context.fillStyle = "#AAA";
        context.fillRect(0, 0, canvas.width, canvas.height);
        
        const data = canvas.toDataURL("image/png");
        photo.setAttribute("src", data);
    }
    
    // Capture a photo by fetching the current contents of the video
    // and drawing it into a canvas, then converting that to a PNG
    // format data URL. By drawing it on an offscreen canvas and then
    // drawing that to the screen, we can change its size and/or apply
    // other changes before drawing it.
    function takePicture() {
        const context = canvas.getContext("2d");
        if (canvas.width && canvas.height) {
            context.drawImage(video, 0, 0, canvas.width, canvas.height);
            context.font = "bold 15pt Calibri";
            context.fillStyle = "white";
            context.fillText(`${lat} | ${long} | ${acc}`, 20, 20);
            
            const data = canvas.toDataURL("image/png");
            photo.setAttribute("src", data);
        } else {
            clearPhoto();
        }
    }
    
    function handleSuccess(stream) {
        const videoTracks = stream.getVideoTracks();

        console.log("Got stream with constraints:", constraints);
        console.log(`Using video device: ${videoTracks[0].label}`);
        window.stream = stream; // make variable available to browser console
        video.srcObject = stream;
        // canvas.height = video.videoHeight / (video.videoWidth / canvas.width);
        
        // Firefox currently has a bug where the height can't be read from
        // the video, so we will make assumptions if this happens.
        
        if (isNaN(canvas.height)) {
            canvas.height = canvas.width / (4 / 3);
        }
        
        video.setAttribute("width", canvas.width);
        video.setAttribute("height", canvas.height);
        streaming = true;
    }
    
    function handleError(error) {
        if (error.name === "OverconstrainedError") {
            errorMsg(`OverconstrainedError: The constraints could not be satisfied by the available devices. Constraints: ${JSON.stringify(constraints)}`);
        } else if (error.name === "NotAllowedError") {
            errorMsg("NotAllowedError: Permissions have not been granted to use your camera and microphone, you need to allow the page access to your devices in order for the demo to work.");
        }
        errorMsg(`getUserMedia error: ${error.name}`, error);
    }
    
    function errorMsg(msg, error) {
        const errorElement = document.querySelector("#errorMsg")!;
        errorElement.innerHTML += `<p>${msg}</p>`;
        if (typeof error !== "undefined") {
            console.error(error);
        }
    }
    
    function flipCamera(e) {
        const tracks = video.srcObject.getVideoTracks();
        
        tracks.forEach((track) => {
            track.stop();
        });
        
        video.srcObject = null;
        window.stream = null;

        isFacingModeUser = !isFacingModeUser;
        constraints = window.constraints = {
            audio: false,
            video: {
                facingMode: isFacingModeUser ? "user" : "environment"
            }
        };
        init(e);
        //     .then(init(e))
        //     .catch(handleError(e));
    }
    
    async function init(e) {
        try {
            const stream = await navigator.mediaDevices.getUserMedia(constraints);
            handleSuccess(stream);
            e.target.disabled = true;
        } catch (e) {
            handleError(e);
        }
    }
    
    onMount(() => {
        let constraints = window.constraints = {
            audio: false,
            video: {
                facingMode: isFacingModeUser ? "user" : "environment"
            }
        };
        let video = window.video = document.getElementById("video")!;
        let canvas = window.canvas = document.getElementById("canvas")!;
        canvas.width = 480;
        canvas.height = 360;
        let photo = document.getElementById("photo")!;
        
        navigator.geolocation.getCurrentPosition(geoSuccess, geoError, geoOptions);
    })
</script>

<button onclick={findLoc}>Debug geo details</button>

<div id="geo-detail" hidden>
    <h1>Your position is: </h1>
    <span>Latitute: {lat}</span><br>
    <span>Longitude: {long}</span><br>
    <span>More or less {acc} meters</span><br>
</div>

<div class="content-area">
    <div id="errorMsg"></div>
    <div class="camera">
        <video id="video" playsinline autoplay>
            Video stream not available.
            <track kind="captions">
            </video>
        </div>
        <button id="button" onclick={e=>init(e)}>Start video</button>
        <button id="button" onclick={takePicture}>Take photo</button>
        <button id="button" onclick={e=>flipCamera(e)}>Flip camera</button>
        <canvas id="canvas"></canvas>
        <div class="output">
            <img id="photo" alt="The screen capture will appear in this box." />
        </div>
    </div>
    
    <style>
        #video {
            border: 1px solid black;
            box-shadow: 2px 2px 3px black;
            width: 320px;
            height: 240px;
        }
        
        #photo {
            border: 1px solid black;
            box-shadow: 2px 2px 3px black;
            width: 320px;
            height: 240px;
        }
        
        #canvas {
            display: none;
        }
        
        .camera {
            width: 340px;
            display: inline-block;
        }
        
        .output {
            width: 340px;
            display: inline-block;
            vertical-align: top;
        }
        
        #button {
            display: block;
            position: relative;
            margin-left: auto;
            margin-right: auto;
            bottom: 32px;
            background-color: rgb(0 150 0 / 50%);
            border: 1px solid rgb(255 255 255 / 70%);
            box-shadow: 0px 0px 1px 2px rgb(0 0 0 / 20%);
            font-size: 14px;
            font-family: "Lucida Grande", "Arial", sans-serif;
            color: rgb(255 255 255 / 100%);
            cursor: pointer;
        }
        
        #button:hover {
            background-color: orange;
        }
        
        .content-area {
            font-size: 16px;
            font-family: "Lucida Grande", "Arial", sans-serif;
            width: 760px;
        }
    </style>
<script module>
    // import Calendar from '@event-calendar/core';
    import TimeGrid from '@event-calendar/time-grid';
    import Interaction from '@event-calendar/interaction';
    
    export var eventList = [
        {id: 1, start: '2025-4-14 8:00', end: '2025-4-14 9:00', display: 'auto', title: 'Team meeting', editable: true},
        {id: 1, start: '2025-4-14 6:30', end: '2025-4-14 7:30', display: 'auto', title: 'UI/UX Survey and Develop Wireframe', editable: true, backgroundColor: '#e1a83a'},
        {id: 1, start: '2025-4-14 10:00', end: '2025-4-14 12:00', display: 'auto', title: 'Frontend/Backend research', editable: true, backgroundColor: '#7fb8d5'},
        {id: 1, start: '2025-4-14 13:00', end: '2025-4-14 14:30', display: 'auto', title: '1:1 meeting w/ Vanessa', editable: true, backgroundColor: 'purple'},
        {id: 2, start: '2025-4-15 8:00', end: '2025-4-15 9:00', display: 'auto', title: 'Team meeting', editable: true},
        {id: 2, start: '2025-4-15 10:00', end: '2025-4-15 13:00', display: 'auto', title: 'Develop UI/UX', editable: true, backgroundColor: 'rgb(230, 110, 127)'},
        {id: 3, start: '2025-4-16 10:00', end: '2025-4-16 12:00', display: 'auto', title: 'UI/UX Survey and Develop Wireframe', editable: true, backgroundColor: '#e1a83a'},
        {id: 3, start: '2025-4-16 7:30', end: '2025-4-16 9:00', display: 'auto', title: '1:1 meeting w/ Brooklyn', editable: true, backgroundColor: 'purple'},
        {id: 3, start: '2025-4-16 13:00', end: '2025-4-16 14:00', display: 'auto', title: 'User Support Meeting', editable: true},
        {id: 4, start: '2025-4-17 8:00', end: '2025-4-17 9:00', display: 'auto', title: 'Team meeting', editable: true},
        {id: 5, start: '2025-4-18 8:00', end: '2025-4-18 9:00', display: 'auto', title: 'Team meeting', editable: true},
    ]
    
    export let plugins = [Interaction, TimeGrid];
    export let options = $state({
        events: eventList,
        view: 'timeGridWeek',
        editable: true,
        styles: 'font-size: 24px; border-radius: 4px',
        eventDurationEditable: true,
        height: '100%',
        eventDragStart: (info) => {
            console.log(info);
        },
        eventClick: (info) => {
            console.log(info);
            if(info.event.id == 1) {
                var newObj = {id:6,start:'2025-4-14 9:00', end:'2025-4-14 10:00', display:'auto', title:'Demo Meeting', backgroundColor: 'rgb(255, 204, 231)', textColor: 'black'};
                eventList.push(newObj);
                options.events = eventList
            }
            else if(info.event.id == 6) {
                var newObj = {id:7,start:'2025-4-14 11:00', end:'2025-4-14 12:00', display:'auto', title:'1:1 Meeting', backgroundColor: 'rgb(255, 204, 231)', textColor: 'black'};
                eventList.push(newObj);
                options.events = eventList
            }
            else if(info.event.id == 7) {
                var newObj = {id:8,start:'2025-4-14 10:00', end:'2025-4-14 11:00', display:'auto', title:'Build Demo', backgroundColor: 'rgb(255, 245, 204)', textColor: 'black'};
                eventList.push(newObj);
                options.events = eventList
            }
        },
        eventMouseLeave: (info) => {
            console.log(info);
        },
        eventDrop: (info) => {
            console.log(info);
        },
    });
    
    export function updateOptions() { 
        //  options.slotDuration = '01:00'; 
        //  alert('hey');
         options.events = [
        // 10/21 - 10/25
            // {id: 1, start: '2025-3-3 7:00', end: '2025-3-3 17:00', display: 'background', title: 'Work Day'},
            // {id: 2, start: '2025-3-4 12:00', end: '2025-3-4 14:00', display: 'background', title: 'Lunch', backgroundColor: 'orange'},
            // {id: 3, start: '2025-3-5 7:00', end: '2025-3-5 17:00', display: 'background', title: 'Work Day'},
            // {id: 4, start: '2025-3-6 12:00', end: '2025-3-6 14:00', display: 'background', title: 'Lunch', backgroundColor: 'orange'},
            // {id: 5, start: '2025-3-7 7:00', end: '2025-3-7 14:00', allDay: true, display: 'background', title: 'Vacation', backgroundColor:'purple'},
            {id: 1, start: '2025-3-24 7:00', end: '2025-3-24 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
            {id: 2, start: '2025-3-25 12:00', end: '2025-3-25 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'grey'},
            {id: 3, start: '2025-3-26 7:00', end: '2025-3-26 17:00', display: 'auto', title: 'Work Day', backgroundColor: 'grey'},
            {id: 4, start: '2025-3-27 12:00', end: '2025-3-27 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'grey'},
            {id: 5, start: '2025-3-28 7:00', end: '2025-3-28 14:00', allDay: true, display: 'auto', title: 'Vacation', backgroundColor: 'grey'},
        ];
    }
    
    export function acceptOptions() {
        options.events = [
        // 10/21 - 10/25
        {id: 1, start: '2025-3-24 7:00', end: '2025-3-24 17:00', display: 'auto', title: 'Work Day', editable: true},
        {id: 2, start: '2025-3-25 12:00', end: '2025-3-25 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange', editable: true},
        {id: 3, start: '2025-3-26 7:00', end: '2025-3-26 17:00', display: 'auto', title: 'Work Day', editable: true},
        {id: 4, start: '2025-3-27 12:00', end: '2025-3-27 14:00', display: 'auto', title: 'Lunch', backgroundColor: 'orange', editable: true},
        {id: 5, start: '2025-3-28 7:00', end: '2025-3-28 14:00', allDay: true, display: 'auto', title: 'Vacation', backgroundColor:'purple', editable: true},
        ];
    }
    
</script>
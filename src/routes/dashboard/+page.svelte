<script lang="ts">
	import { onMount } from "svelte";
	// import { getLocalTimeZone, today } from "@internationalized/date";
	// import Calendar from "$lib/components/ui/calendar/calendar.svelte";
	import Tasklist from "$lib/components/tasklist.svelte";
	import Communityforum from "$lib/components/communityforum.svelte";
	import Rewards from "$lib/components/rewards.svelte";
	import Calendar from '@event-calendar/core';
	import { plugins, options } from '$lib/components/calendar.svelte';
	options.height = '95%';
	
	// let value = today(getLocalTimeZone());

	onMount(() => {
		document.getElementById('calendar-div')!.childNodes[0].style.width='95%';
	});
</script>

<header class="flex h-8 shrink-0 items-center gap-2 transition-[width,height] ease-linear group-has-[[data-collapsible=icon]]/sidebar-wrapper:h-12">
</header>
<div class="flex flex-1 flex-col gap-4 p-4 pt-0 h-dvh">
	<div class="grid auto-rows-min gap-4 md:grid-cols-3">
		<div class="flex justify-center items-center bg-muted/50 aspect-video rounded-xl overflow-y-scroll">
			<Tasklist />
		</div>
		<div class="flex flex-col justify-center items-center bg-muted/50 aspect-video rounded-xl">
			<h1>Community Forums</h1>
			<Communityforum />
		</div>
		<div class="flex flex-col justify-center items-center bg-muted/50 aspect-video rounded-xl">
			<h1>Points & Rewards</h1>
			<Rewards />
		</div>
	</div>
	<div id="calendar-div" class="flex flex-col justify-top items-center max-h-[36rem] bg-muted/50 rounded-xl md:min-h-min">
		<Calendar {plugins} {options}/>
	</div>
</div>
<script lang="ts">
	// import { getLocalTimeZone, today } from "@internationalized/date";
	import Calendar from "$lib/components/ui/calendar/calendar.svelte";
	// import Calendar from '@event-calendar/core';
	// import { plugins, options } from '$lib/components/calendar.svelte';
	
	// let value = today(getLocalTimeZone());

</script>

<header class="flex h-16 shrink-0 items-center gap-2 transition-[width,height] ease-linear group-has-[[data-collapsible=icon]]/sidebar-wrapper:h-12">
</header>
<div class="flex flex-1 flex-col gap-4 p-4 pt-0">
	<div class="grid auto-rows-min gap-4 md:grid-cols-3">
		<div class="flex justify-center items-center bg-muted/50 aspect-video rounded-xl">
			<div>Task List</div>
		</div>
		<div class="flex justify-center items-center bg-muted/50 aspect-video rounded-xl">
			<div>Community Forums</div>
		</div>
		<div class="flex justify-center items-center bg-muted/50 aspect-video rounded-xl">
			<div>Points and Rewards</div>
		</div>
	</div>
	<div class="flex flex-col justify-center items-center bg-muted/50 min-h-[100vh] flex-1 rounded-xl md:min-h-min">
		<!-- <Calendar {plugins} {options}/> -->
		<Calendar />
	</div>
</div>
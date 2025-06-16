<script lang="ts">
    import { plugins, options, eventList } from '$lib/components/calendar.svelte';
    import Calendar from '@event-calendar/core';
</script>

<div class="p-10 h-dvh">
    <Calendar {plugins} {options} />
</div>
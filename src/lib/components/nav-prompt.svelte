<script>
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
  	import { Textarea } from "$lib/components/ui/textarea/index.js";
	import { Button } from "$lib/components/ui/button/index.js";
	import { updateOptions, acceptOptions } from "$lib/components/calendar.svelte";

	let suggest = $state(true);
</script>

<Sidebar.Group class="group-data-[collapsible=icon]:hidden grid w-full gap-2">
	<Sidebar.GroupLabel>Prompt</Sidebar.GroupLabel>
	<Textarea placeholder="Enter your prompt here"></Textarea>
	{#if suggest}
		<Button onclick={() => {updateOptions(), suggest = !suggest}}>Ask Harmony</Button>
	{:else}
		<Button variant="destructive" onclick={() => {acceptOptions(), suggest = !suggest}}>Accept suggestions</Button>  
		<Button variant="secondary" onclick={() => {acceptOptions(), suggest = !suggest}}>Try again</Button>  
	{/if}
</Sidebar.Group>

<script lang="ts">
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
    // let items = $props();

    let {
		items,
	}: {
		items: {
            url: string;
			item: string;
		}[];
	} = $props();
    $inspect(items);
</script>

<Sidebar.Group>
	<Sidebar.GroupLabel>Notifications<span class="inline-flex ml-2 items-center rounded-md bg-red-50 px-2 py-1 text-xs font-medium text-red-700 ring-1 ring-red-600/10 ring-inset">{items.length}</span></Sidebar.GroupLabel>
        {#each items as update (update.item)}
            <a href={update.url} class="hover:bg-red-50 rounded-lg">
                <ul class="list-disc px-5">
                    <li>{update.item}</li>
                </ul>
            </a>
        {/each}
</Sidebar.Group>

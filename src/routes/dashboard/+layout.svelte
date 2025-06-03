<script lang="ts">
	import { base } from '$app/paths';
	import { page } from '$app/state';
	import AppSidebar from "$lib/components/app-sidebar.svelte";
	import * as Breadcrumb from "$lib/components/ui/breadcrumb/index.js";
	import { Separator } from "$lib/components/ui/separator/index.js";
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
	let { children } = $props ();

	let breadcrumbList = $state(page.url.pathname.split('/').filter(Boolean));
	console.log(breadcrumbList);
</script>
<Sidebar.Provider>
	<AppSidebar />
	<Sidebar.Inset>
		<div class="flex items-center gap-2 px-4">
			<Sidebar.Trigger class="-ml-1" />
			<!--- Separator orientation="vertical" class="mr-2 h-4" />
			<Breadcrumb.Root> 
				<Breadcrumb.List>
					{#each breadcrumbList as item, index}
						{#if breadcrumbList.length - 1 == index}
							<Breadcrumb.Item>
								<Breadcrumb.Link href="{base}/{item}">{item}</Breadcrumb.Link>
							</Breadcrumb.Item>
						{:else}
							<Breadcrumb.Item class="hidden md:block">
								<Breadcrumb.Link href="{base}{(item == 'dashboard') ? '' : 'dashboard' }/{item}">{item}</Breadcrumb.Link>
							</Breadcrumb.Item>
							<Breadcrumb.Separator class="hidden md:block" />
						{/if}
					{/each}
				</Breadcrumb.List>
			</Breadcrumb.Root --->
		</div>
		{@render children()}
	</Sidebar.Inset>
</Sidebar.Provider>
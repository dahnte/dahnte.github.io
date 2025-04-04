<script lang="ts">
	import * as Collapsible from "$lib/components/ui/collapsible/index.js";
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
	import ChevronRight from "lucide-svelte/icons/chevron-right";
    import { toggleMode } from "mode-watcher";
	// import { Badge } from "$lib/components/ui/badge/index.js";

	let {
		items,
	}: {
		items: {
			title: string;
			url: string;
			// this should be `Component` after lucide-svelte updates types
			// eslint-disable-next-line @typescript-eslint/no-explicit-any
			icon?: any;
			isActive?: boolean;
			items?: {
				title: string;
				url: string;
				toggleSwitch?: boolean;
			}[]
		}[];
	} = $props();
</script>

<Sidebar.Group>
	<Sidebar.GroupLabel>Apps</Sidebar.GroupLabel>
	<Sidebar.Menu>
		{#each items as mainItem (mainItem.title)}
			<Collapsible.Root open={mainItem.isActive} class="group/collapsible">
				{#snippet child({ props })}
					<Sidebar.MenuItem {...props}>
						<Collapsible.Trigger>
							{#snippet child({ props })}
							{#if mainItem.items}
								<Sidebar.MenuButton {...props}>
								{#snippet tooltipContent()}
									{mainItem.title}
								{/snippet}
								{#if mainItem.icon}
									<mainItem.icon />
								{/if}
								<span>{mainItem.title}</span>
								<ChevronRight
									class="ml-auto transition-transform duration-200 group-data-[state=open]/collapsible:rotate-90"
								/>
								</Sidebar.MenuButton>
							{:else}
								<a href={mainItem.url}>
								<Sidebar.MenuButton {...props}>
									{#snippet tooltipContent()}
										{mainItem.title}
									{/snippet}
									{#if mainItem.icon}
										<mainItem.icon />
									{/if}
									<span>{mainItem.title}</span>
								</Sidebar.MenuButton>
								</a>
							{/if}
							{/snippet}
						</Collapsible.Trigger>
						<Collapsible.Content>
							{#if mainItem.items}
								<Sidebar.MenuSub>
									{#each mainItem.items as subItem (subItem.title)}
										<Sidebar.MenuSubItem>
											<Sidebar.MenuSubButton>
												{#snippet child({ props })}
													{#if subItem.toggleSwitch}
													<a href={subItem.url} onclick={toggleMode} {...props}>
														<span>{subItem.title}</span>
													</a>
													{:else}
													<a href={subItem.url} {...props}>
														<span>{subItem.title}</span>
													</a>
													{/if}
												{/snippet}
											</Sidebar.MenuSubButton>
										</Sidebar.MenuSubItem>
									{/each}
								</Sidebar.MenuSub>
							{/if}
						</Collapsible.Content>
					</Sidebar.MenuItem>
				{/snippet}
			</Collapsible.Root>
		{/each}
	</Sidebar.Menu>
</Sidebar.Group>

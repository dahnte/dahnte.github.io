<script lang="ts">
    import * as Sidebar from "$lib/components/ui/sidebar/index.js";
    import * as Collapsible from "$lib/components/ui/collapsible/index.js";
	import ChevronRight from "lucide-svelte/icons/chevron-right";
    import { Badge } from "$lib/components/ui/badge/index.js";
    import BadgeCheckIcon from "@lucide/svelte/icons/badge-check";
    // let items = $props();
    
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
				message: string;
				url: string;
			}[]
		}[];
	} = $props();

    // let {
    //     items,
    // }: {
    //     items: {
    //         url: string;
    //         item: string;
    //     }[];
    // } = $props();
    $inspect(items);
</script>

<Sidebar.Group>
	<Sidebar.Menu>
		{#each items as mainItem (mainItem.title)}
			<Collapsible.Root open={mainItem.isActive} class="group/collapsible">
				{#snippet child({ props })}
					<Sidebar.MenuItem {...props}>
						<Collapsible.Trigger>
							{#snippet child({ props })}
								<Sidebar.MenuButton {...props}>
								{#snippet tooltipContent()}
									{mainItem.items!.length} unread notifications
								{/snippet}
									<Badge class="h-5 min-w-5 rounded-full px-1 font-mono tabular-nums" variant="destructive">
                                        {mainItem.items!.length}
                                    </Badge>
									<!-- <mainItem.icon /> -->
								<span>
                                    {mainItem.title}
                                </span>
								<ChevronRight
									class="ml-auto transition-transform duration-200 group-data-[state=open]/collapsible:rotate-90"
								/>
								</Sidebar.MenuButton>
							{/snippet}
						</Collapsible.Trigger>
						<Collapsible.Content>
							{#if mainItem.items}
								<Sidebar.MenuSub>
									{#each mainItem.items as subItem (subItem.message)}
										<Sidebar.MenuSubItem>
											<Sidebar.MenuSubButton>
												{#snippet child({ props })}
													<a href={subItem.url} {...props}>
														<span>{subItem.message}</span>
													</a>
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
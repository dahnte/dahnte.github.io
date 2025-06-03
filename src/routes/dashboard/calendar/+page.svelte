<script lang="ts">
    import { onMount } from 'svelte';
    import { plugins, options, eventList } from '$lib/components/calendar.svelte';
    import { Button } from "$lib/components/ui/button/index.js";
    import * as Drawer from "$lib/components/ui/drawer/index.js";
    import Calendar from '@event-calendar/core';
    import { draggable, droppable, type DragDropState } from '@thisux/sveltednd';
	import { fade } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	interface Item {
		id: string;
		title: string;
		description: string;
		priority: 'low' | 'medium' | 'high';
	}

    // let container1 = $state<Item[]>([
	// 	{ id: 'a', name: 'Frontend research' },
	// 	{ id: 'b', name: 'Emails' }
	// ]);

	// let container2 = $state<Item[]>([
	// 	{ id: 'c', name: 'Demo meeting' },
	// 	{ id: 'd', name: 'Build demo' }
	// ]);

    // interface Item {
	// 	id: string;
	// 	name: string;
	// }

    // function handleDrop(state: DragDropState<Item>) {
	// 	const { sourceContainer, targetContainer, draggedItem } = state;

	// 	if (sourceContainer === 'container1') {
	// 		container1 = container1.filter((i) => i.id !== draggedItem.id);
	// 		container2 = [...container2, draggedItem];
	// 	} else {
	// 		container2 = container2.filter((i) => i.id !== draggedItem.id);
	// 		container1 = [...container1, draggedItem];
	// 	}
	// }

	const items = $state<Item[]>([
		{
			id: '1',
			title: 'Database integration',
			description: 'Backend workload',
			priority: 'high'
		},
        {
			id: '5',
			title: 'Develop UI/UX',
			description: 'Frontend workload',
			priority: 'high'
		},
		{
			id: '2',
			title: 'UI/UX Survey and Develop Wireframe',
			description: 'Review feedback given from user testing',
			priority: 'medium'
		},
		{
			id: '3',
			title: 'Frontend/backend research',
			description: 'Look into best practices for security and performance',
			priority: 'low'
		},
        {
			id: '4',
			title: 'API integration research',
			description: 'Look into cost effective/practical integrations',
			priority: 'low'
		}

	]);
    // const items2 = $state<Item[]>([
    //     {
    //         id: '5',
    //         title: 'Blank',
    //         description: 'Try',
    //         priority: 'low'
    //     }
	// ]);

	function handleDrop(state: DragDropState<Item>) {
		const { draggedItem, targetContainer } = state;
		const dragIndex = items.findIndex((item: Item) => item.id === draggedItem.id);
		const dropIndex = parseInt(targetContainer ?? '0');

		if (dragIndex !== -1 && !isNaN(dropIndex)) {
			const [item] = items.splice(dragIndex, 1);
			items.splice(dropIndex, 0, item);
		}
	}

	function handleDropTask() {
		console.log("TEST DROP!");

		if(tracker == 0) {
			eventList.push({id: 1, start: '2025-4-17 6:30', end: '2025-4-17 7:30', display: 'auto', title: 'API integration research', editable: true, backgroundColor: '#7fb8d5'});
			options.events = eventList;
			tracker = 1;
		} else if (tracker == 1) {
			eventList.push({id: 2, start: '2025-4-17 10:00', end: '2025-4-17 13:00', display: 'auto', title: 'Database integration', editable: true, backgroundColor: 'rgb(230, 110, 127)'});
			options.events = eventList;
			tracker = 2;
		} else if (tracker == 2) {
			eventList.push({id: 1, start: '2025-4-18 6:30', end: '2025-4-18 7:30', display: 'auto', title: 'UI/UX Survey and Develop Wireframe', editable: true, backgroundColor: '#e1a83a'});
			options.events = eventList;
			tracker = 3;
		} else if (tracker == 3) {
			eventList.push({id: 2, start: '2025-4-18 12:00', end: '2025-4-18 14:00', display: 'auto', title: 'Develop UI/UX', editable: true, backgroundColor: 'rgb(230, 110, 127)'});
			options.events = eventList;
			tracker = 4;
		} else if (tracker == 4) {
			eventList.push({id: 2, start: '2025-4-18 10:00', end: '2025-4-18 11:00', display: 'auto', title: 'Frontend/Backend research', editable: true, backgroundColor: '#7fb8d5'});
			options.events = eventList;
			tracker = 5;
		}
	}

	const getPriorityColor = (priority: Item['priority']) => {
		return {
			low: 'bg-blue-50 text-blue-700',
			medium: 'bg-yellow-50 text-yellow-700',
			high: 'bg-red-50 text-red-700'
		}[priority];
	};

	const dragStyles = {
		low: 'bg-gradient-to-r from-sky-400/30 via-blue-400/20 to-indigo-400/30 backdrop-blur-lg',
		medium: 'bg-gradient-to-r from-amber-400/30 via-orange-400/20 to-yellow-400/30 backdrop-blur-lg',
		high: 'bg-gradient-to-r from-rose-400/30 via-red-400/20 to-pink-400/30 backdrop-blur-lg'
	};

    onMount(() => {
        document.getElementById('drawerTrigger')!.click();
    });
</script>

<Drawer.Root>
    <Drawer.Trigger class="hidden" id="drawerTrigger" >Open</Drawer.Trigger>
    <Drawer.Content>
        <Drawer.Header>
            <Drawer.Title>Build Your Own Schedule</Drawer.Title>
            <Drawer.Description>Simply drag-and-drop tasks into your work week.</Drawer.Description>
        </Drawer.Header>
        <Drawer.Footer>
            <div class="max-h-screen bg-gradient-to-br from-slate-50 to-gray-100 p-8 flex flex-row">
                <div class="w-80">
                    <div class="rounded-xl bg-white/40 p-4 shadow-lg ring-1 ring-white/60 backdrop-blur-xl">
                        <div class="space-y-4">
                            {#each items as item, index (item.id)}
                                <div
                                    use:draggable={{ container: index.toString(), dragData: item }}
                                    use:droppable={{
                                        container: index.toString(),
                                        callbacks: { onDrop: handleDrop },
                                        attributes: {
                                            draggingClass: 'scale-105 rotate-2 !shadow-2xl !ring-2 ring-blue-500/50 z-50',
                                            dragOverClass: 'scale-98 -rotate-1 !shadow-inner !ring-2 ring-emerald-500/50'
                                        }
                                    }}
                                    animate:flip={{ duration: 400, easing: 'cubic-bezier(0.4, 0, 0.2, 1)' }}
                                    in:fade={{ duration: 300 }}
                                    out:fade={{ duration: 200 }}
                                    class="group relative cursor-move rounded-lg p-4
                                           shadow-md ring-1 ring-white/60
                                           backdrop-blur-md transition-all duration-500
                                           ease-out hover:-rotate-1 hover:scale-[1.02]
                                           hover:shadow-xl active:shadow-inner
                                           {dragStyles[item.priority]}">
                                    <div class="relative overflow-hidden rounded-md">
                                        <div
                                            class="absolute inset-0 bg-gradient-to-br from-white/10 via-transparent to-white/20 opacity-0
                                                  transition-all duration-500 group-hover:opacity-100"
                                        ></div>
                                        <div class="relative z-10 space-y-2">
                                            <div class="flex items-start justify-between">
                                                <h3 class="font-medium text-gray-900">{item.title}</h3>
                                                <span
                                                    class="inline-flex items-center rounded-md px-2 py-1 text-xs font-medium {getPriorityColor(item.priority)}">
                                                    {item.priority}
                                                </span>
                                            </div>
                                            <p class="text-sm text-gray-600">{item.description}</p>
                                        </div>
                                    </div>
                                </div>
                            {/each}
                        </div>
                    </div>
                </div>
                <div class="px-10 h-[37rem] w-full overflow-auto" 
				use:droppable={{ container: 'tester', callbacks: { onDrop: handleDropTask }}}>
                    <Calendar {plugins} {options} />
                </div>
            </div>
            <!--- div class="flex gap-4">
                <div use:droppable={{ container: 'container1', callbacks: { onDrop: handleDrop } }}>
                    {#each container1 as item}
                        <div use:draggable={{ container: 'container1', dragData: item }}>
                            {item.name}
                        </div>
                    {/each}
                </div>
            
                <div use:droppable={{ container: 'container2', callbacks: { onDrop: handleDrop } }}>
                    {#each container2 as item}
                        <div use:draggable={{ container: 'container2', dragData: item }}>
                            {item.name}
                        </div>
                    {/each}
                </div>
            </div --->
            <Button>Submit</Button>
            <Drawer.Close>Cancel</Drawer.Close>
        </Drawer.Footer>
    </Drawer.Content>
</Drawer.Root>
<div class="p-10 h-dvh">
    <Calendar {plugins} {options} />
</div>

<style>
	:global(.dragging) {
		@apply opacity-60;
		animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
	}

	@keyframes pulse {
		0%,
		100% {
			opacity: 0.6;
		}
		50% {
			opacity: 0.8;
		}
	}

	:global(.drag-over) {
		@apply bg-blue-50;
	}

	/* Add custom scaling utility */
	.scale-102 {
		transform: scale(1.02);
	}
	.scale-98 {
		transform: scale(0.98);
	}
</style>
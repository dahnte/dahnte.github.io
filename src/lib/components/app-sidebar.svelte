<script lang="ts" module>
	import AudioWaveform from "lucide-svelte/icons/audio-waveform";
	import BookOpen from "lucide-svelte/icons/book-open";
	import Bot from "lucide-svelte/icons/bot";
	import ChartPie from "lucide-svelte/icons/chart-pie";
	import Command from "lucide-svelte/icons/command";
	import Frame from "lucide-svelte/icons/frame";
	import GalleryVerticalEnd from "lucide-svelte/icons/gallery-vertical-end";
	import Map from "lucide-svelte/icons/map";
	import Settings2 from "lucide-svelte/icons/settings-2";
	import SquareTerminal from "lucide-svelte/icons/square-terminal";
	import CalendarDays from "lucide-svelte/icons/calendar-days";
	import ListTodo from  "lucide-svelte/icons/list-todo";
	import Blocks from "lucide-svelte/icons/blocks";
	import { base } from "$app/paths";
	import evenLogo from "$lib/evenLogo.png";
	
	// This is sample data.
	const data = {
		user: {
			name: "Dante",
			email: "dante@evenworks.us",
			avatar: "",
		},
		teams: [
		{
			name: "Evenworks",
			logo: evenLogo,
			plan: "Free",
		},
		],
		navMain: [
		{
			title: "Calendar",
			url: base + "/dashboard/calendar",
			icon: CalendarDays,
			// items: [
			// 	{
			// 		title: "Duo View",
			// 		url: base + "/dashboard/duo",
			// 	},
			// 	{
			// 		title: "Build Your Own Schedule",
			// 		url: base + "/dashboard/byos",
			// 	},
			// ],
		},
		{
			title: "Tasklist",
			url: base + "/dashboard/tasklist",
			icon: ListTodo,
		},
		{
			title: "Build Your Own Schedule",
			url: base + "/dashboard/tasklist",
			icon: Blocks,
		},
		{
			title: "Settings",
			url: base + "/dashboard",
			icon: Settings2,
			items: [
			{
				title: "General",
				url: "#",
			},
			{
				title: "Team",
				url: "#",
			},
			{
				title: "Billing",
				url: "#",
			},
			{
				title: "Limits",
				url: "#",
			},
			{
				title: "Toggle theme",
				url: "#",
				toggleSwitch: true,
			},
			],
		},
		],
		// navNotif: [
		// 	{
		// 		url: base + "/dashboard/calendar",
		// 		item: "Your meeting has been rescheduled for Monday at 8:30 AM",
		// 	},
		// 	{
		// 		url: base + "/dashboard/tasklist",
		// 		item: "You have pending tasks that need to be reviewed",
		// 	},
		// ],
		navNotif: [
			{
				title: "Notifications",
				icon: Settings2,
				items: [
					{
						message: "Your meeting has been rescheduled for Monday at 8:30 AM",
						url: "#",
					},
					{
						message: "You have pending tasks that need to be reviewed",
						url: "#",
					},
				],
			},
		]
	};
</script>

<script lang="ts">
	import NavMain from "$lib/components/nav-main.svelte";
	import NavPrompt from "$lib/components/nav-prompt.svelte";
	import NavUser from "$lib/components/nav-user.svelte";
	import NavNotif from "$lib/components/nav-notif.svelte";
	import TeamSwitcher from "$lib/components/team-switcher.svelte";
	import * as Sidebar from "$lib/components/ui/sidebar/index.js";
	import type { ComponentProps } from "svelte";
	
	let {
		ref = $bindable(null),
		collapsible = "icon",
		...restProps
	}: ComponentProps<typeof Sidebar.Root> = $props();
	</script>
	
	<Sidebar.Root bind:ref {collapsible} {...restProps}>
		<Sidebar.Header>
			<TeamSwitcher teams={data.teams} />
		</Sidebar.Header>
		<Sidebar.Content>
			<NavNotif items={data.navNotif} />
			<NavPrompt />
			<NavMain items={data.navMain} />
		</Sidebar.Content>
		<Sidebar.Footer>
			<NavUser user={data.user} />
		</Sidebar.Footer>
		<Sidebar.Rail />
	</Sidebar.Root>
	
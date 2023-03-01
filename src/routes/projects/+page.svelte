<script lang="ts">
	import { Badge, Card, Img } from 'flowbite-svelte';
	import { CodeSolid, GithubBrand, LinkSolid } from 'svelte-awesome-icons';

	enum ItemType {
		Card,
		Section
	}

	let items = [
		{
			type: ItemType.Card,
			title: 'Shamrock Cluster',
			headImg: '/images/shamrock-cluster-light.png',
			headImgDark: '/images/shamrock-cluster-dark.png',
			headImgAlt: 'Shamrock Cluster',
			hideTitle: true,
			description:
				'<p>"Production" lab environment featuring <b>Proxmox VE, Ceph, and Kubernetes</b>.</p>' +
				'<p class="mt-2">Find out more on the <b>wiki</b>&nbsp;&raquo;</p>',
			img: '/images/cluster.jpg',
			href: 'https://shamrock.systems',
			icon: LinkSolid
		},
		{
			type: ItemType.Card,
			title: 'Shamrock Sixnav',
			headImg: '/images/shamrock-sixnav-full-light.png',
			headImgDark: '/images/shamrock-sixnav-full-dark.png',
			headImgAlt: 'Shamrock Sixnav',
			hideTitle: true,
			description:
				'<p>6 Degree of Freedom (6DOF) Optical sensor-based human input device for CAD software</p>' +
				'<p class="mt-2">Find out more on <b>Github</b>&nbsp;&raquo;</p>',
			img: '/images/sixnav-photo.jpg',
			href: 'https://github.com/GreenCappuccino/SixnavPrototype',
			icon: GithubBrand
		},
		{
			type: ItemType.Card,
			title: 'Sequoia',
			description:
				'<p>Flexible asynchronous task scheduler for FIRST Tech Challenge robotics SDK.</p>' +
				'<ul class="list-disc list-inside my-2">' +
				'<li><b>Synchronizes</b> and <b>prioritizes</b> subsystem control loops</li>' +
				'<li>Schedules and controls <b>lifetime</b> of individual tasks that operate on subsystems</li>' +
				'<li>Fuses positioning data from <b>computer vision</b> and <b>dead reckoning</b> systems</li>' +
				'<li>Handles player input during multiple subroutine execution</li>' +
				'</ul><p>Find out more on <b>Github</b>&nbsp;&raquo;</p>',
			img: '/images/robot.jpg',
			href: 'https://github.com/HighOakRobotics/Sequoia',
			icon: GithubBrand
		},
		{ type: ItemType.Section, title: 'Hackathons' },
		{
			type: ItemType.Card,
			title: 'VaxFinder',
			badge: 'First Place',
			description:
				'<p>Fetches COVID-19 vaccine availability data from over 29,000 locations every 15 seconds. ' +
				'Geolocates user by street address, and notifies them via call when vaccines are available near them.</p>' +
				'<p class="mt-2">Find out more on <b>Devpost</b>&nbsp;&raquo;</p>',
			img: '/images/vaxfinder-1024.png',
			href: 'https://devpost.com/software/vaxfinder?ref_content=user-portfolio&ref_feature=in_progress',
			icon: CodeSolid
		},
		{
			type: ItemType.Card,
			title: 'Notus',
			badge: 'Best Future Impact',
			description:
				'<p>Monte Carlo simulations of COVID-19 particle spread through various room layouts.</p>' +
				'<p class="mt-2">Find out more on <b>Devpost</b>&nbsp;&raquo;</p>',
			img: '/images/notus.png',
			href: 'https://devpost.com/software/covid-room-designer',
			icon: CodeSolid
		}
	];
</script>

<svelte:head>
	<title>Projects | Brian Lu</title>
</svelte:head>

{#each items as item, itemIndex}
	{#if item.type === ItemType.Card}
		<Card img={item.img} href={item.href} horizontal>
			{#if item.icon}
				<svelte:component this={item.icon} class="ml-auto" />
			{/if}
			<div class="mr-auto">
				{#if item.headImg}
					<Img
						src={item.headImg}
						size="w-96 h-auto"
						alignment="mb-2"
						class={item.headImgDark ? 'dark:hidden' : null}
						alt={item.headImgAlt}
					/>
				{/if}
				{#if item.headImgDark}
					<Img
						src={item.headImgDark}
						size="w-96 h-auto"
						alignment="mb-2"
						class="hidden dark:block"
						alt={item.headImgAlt}
					/>
				{/if}
				{#if item.title && !item.hideTitle}
					<div class="flex flex-row items-center ">
						<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
							{item.title}
						</h5>
						{#if item.badge}
							<Badge color="green" class="ml-2">{item.badge}</Badge>
						{/if}
					</div>
				{/if}
			</div>
			{#if item.description}
				<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
					{@html item.description}
				</p>
			{/if}
		</Card>
	{:else if item.type === ItemType.Section}
		<h4 class="mb-2 text-3xl font-bold tracking-tight text-gray-900 dark:text-white">
			{item.title}
		</h4>
	{/if}
	{#if itemIndex < items.length - 1}
		<div class="m-2" />
	{/if}
{/each}

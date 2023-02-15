<script lang="ts">
	import '../app.css';
	import {
		Button,
		ButtonGroup,
		Card,
		CloseButton,
		Drawer,
		Footer,
		FooterCopyright,
		FooterLink,
		FooterLinkGroup,
		Heading,
		Hr,
		Sidebar,
		SidebarGroup,
		SidebarItem,
		SidebarWrapper
	} from 'flowbite-svelte';
	import { sineIn } from 'svelte/easing';
	import DarkMode from '$lib/components/DarkMode.svelte';
	import {
		BarsSolid,
		GraduationCapSolid,
		HouseChimneySolid,
		KeySolid,
		PaintbrushSolid,
		RectangleListSolid
	} from 'svelte-awesome-icons';

	let links = [
		{ href: '/', name: 'Home', icon: HouseChimneySolid },
		{ href: '/projects', name: 'Projects', icon: RectangleListSolid },
		{ href: '/education', name: 'Education', icon: GraduationCapSolid },
		{ href: '/design', name: 'Design', icon: PaintbrushSolid },
		{ href: '/keys', name: 'Keys', icon: KeySolid }
	];
	let hideDrawer = true;
	let drawerTransitionParams = {
		x: -320,
		duration: 200,
		easing: sineIn
	};
</script>

<svelte:head>
	<script>
		if (window) {
			localStorage.getItem('color-theme') === 'dark' ||
			(!('color-theme' in localStorage) &&
				window.matchMedia('(prefers-color-scheme: dark)').matches)
				? window.document.documentElement.classList.add('dark')
				: window.document.documentElement.classList.remove('dark');
		}
	</script>
</svelte:head>

<div class="flex flex-col items-center text-center min-h-screen bg-gray-100 dark:bg-black">
	<div class="m-10 w-full" />
	<a href="/">
		<Heading class="mb-2" customSize="text-4xl font-extrabold  md:text-5xl lg:text-6xl" tag="h1">
			Brian Lu
		</Heading>
	</a>
	<Heading
		class="mb-4 dark:text-gray-400"
		customSize="text-lg lg:text-xl sm:px-16 xl:px-48"
		tag="h2"
	>
		Test tagline please ignore
	</Heading>
	<ButtonGroup class="mr-5 mb-4 justify-center items-center hidden sm:flex">
		{#each links as link}
			<Button href={link.href}>
				{#if link.icon}
					<svelte:component this={link.icon} size="1em" class="mr-2" />
				{/if}
				{link.name}
			</Button>
		{/each}
		<DarkMode />
	</ButtonGroup>
	<div class="mb-4 ml-2 mr-2 flex flex-row flex-wrap justify-center space-x-2 sm:hidden">
		<Button class="mt-1 mb-1" color="alternative" on:click={() => (hideDrawer = false)}>
			<BarsSolid class="mr-2" size="1em" />
			Menu
		</Button>
		<Button class="mt-1 mb-1" color="alternative" href="/">
			<HouseChimneySolid class="mr-2" size="1em" />
			Home
		</Button>
		<DarkMode buttonClass="mt-1 mb-1" />
	</div>
	<Card class="text-left mb-6 ml-2 mr-2" size="lg">
		<slot />
	</Card>
	<Footer customClass="flex flex-col" footerType="custom">
		<FooterCopyright by="Brian Lu" year={2023} />
		<Hr divClass="mt-2 mb-2" />
		<FooterLinkGroup
			ulClass="flex flex-wrap items-center ml-2 mr-2 mb-10 text-sm text-gray-500 dark:text-gray-400 sm:mt-0"
		>
			{#each links as link}
				<FooterLink href={link.href}>{link.name}</FooterLink>
			{/each}
		</FooterLinkGroup>
	</Footer>
	<Drawer
		bind:hidden={hideDrawer}
		id="sidebar"
		transitionParams={drawerTransitionParams}
		transitionType="fly"
		width="w-30"
	>
		<div class="flex items-center">
			<h5
				class="text-base font-semibold text-gray-500 uppercase dark:text-gray-400"
				id="drawer-navigation-label-3"
			>
				Menu
			</h5>
			<CloseButton class="mb-4 dark:text-white" on:click={() => (hideDrawer = true)} />
		</div>
		<Sidebar>
			<SidebarWrapper divClass="overflow-y-auto py-4 px-3 rounded dark:bg-gray-800">
				<SidebarGroup>
					{#each links as link}
						<SidebarItem label={link.name} href={link.href} on:click={() => (hideDrawer = true)}>
							<svelte:component this={link.icon} slot="icon" />
						</SidebarItem>
					{/each}
				</SidebarGroup>
			</SidebarWrapper>
		</Sidebar>
		<Hr />
		<div class="flex flex-col items-center mt-4">
			<div class="flex flex-row items-center">
				<p class="dark:text-white mr-2">Toggle Dark Mode</p>
				<DarkMode />
			</div>
		</div>
	</Drawer>
</div>

<script lang="ts">
	import '../app.css';
	import {
		Card,
		CloseButton,
		Drawer,
		Heading,
		Footer,
		FooterCopyright,
		FooterLinkGroup,
		FooterLink,
		Sidebar,
		SidebarWrapper,
		SidebarGroup,
		SidebarItem,
		Hr,
		ButtonGroup,
		Button
	} from 'flowbite-svelte';
	import * as Icon from 'svelte-awesome-icons';
	import { sineIn } from 'svelte/easing';
	import DarkMode from '$lib/components/DarkMode.svelte';

	let links = [
		{ href: '/', name: 'Home', icon: Icon.HouseChimneySolid },
		{ href: '/projects', name: 'Projects', icon: Icon.RectangleListSolid },
		{ href: '/education', name: 'Education', icon: Icon.GraduationCapSolid },
		{ href: '/design', name: 'Design', icon: Icon.PaintbrushSolid },
		{ href: '/keys', name: 'Keys', icon: Icon.KeySolid }
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
		<Heading tag="h1" class="mb-2" customSize="text-4xl font-extrabold  md:text-5xl lg:text-6xl">
			Brian Lu
		</Heading>
	</a>
	<Heading
		tag="h2"
		class="mb-4 dark:text-gray-400"
		customSize="text-lg lg:text-xl sm:px-16 xl:px-48"
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
	<div class="mb-4 flex flex-row space-x-2 sm:hidden">
		<Button color="alternative" on:click={() => (hideDrawer = false)}>
			<Icon.BarsSolid size="1em" class="mr-2" />
			Menu
		</Button>
		<Button color="alternative" href="/">
			<Icon.HouseChimneySolid size="1em" class="mr-2" />
			Home
		</Button>
		<DarkMode />
	</div>
	<Card class="text-left mb-6 ml-2 mr-2" size="lg">
		<slot />
	</Card>
	<Footer footerType="custom" customClass="flex flex-col">
		<FooterCopyright by="Brian Lu" year={2023} />
		<Hr divClass="mt-2 mb-2" />
		<FooterLinkGroup
			ulClass="flex flex-wrap items-center mt-5 ml-2 mr-2 text-sm text-gray-500 dark:text-gray-400 sm:mt-0"
		>
			{#each links as link}
				<FooterLink href={link.href}>{link.name}</FooterLink>
			{/each}
		</FooterLinkGroup>
	</Footer>
	<Drawer
		transitionType="fly"
		transitionParams={drawerTransitionParams}
		bind:hidden={hideDrawer}
		id="sidebar2"
	>
		<div class="flex items-center">
			<h5
				id="drawer-navigation-label-3"
				class="text-base font-semibold text-gray-500 uppercase dark:text-gray-400"
			>
				Menu
			</h5>
			<CloseButton on:click={() => (hideDrawer = true)} class="mb-4 dark:text-white" />
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
	</Drawer>
</div>

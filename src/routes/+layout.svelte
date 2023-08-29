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
		Popover,
		Sidebar,
		SidebarGroup,
		SidebarItem,
		SidebarWrapper
	} from 'flowbite-svelte';
	import { sineIn } from 'svelte/easing';
	import DarkMode from '$lib/components/DarkMode.svelte';
	import { Icon } from 'svelte-awesome';
	import {
		faBars,
		faEnvelope,
		faGraduationCap,
		faHouseChimney,
		faKey,
		faPaintbrush,
		faRectangleList
	} from '@fortawesome/free-solid-svg-icons';
	import { faGithub, faLinkedin } from '@fortawesome/free-brands-svg-icons';

	let links = [
		{ href: '/', name: 'Home', icon: faHouseChimney },
		{ href: '/projects', name: 'Projects', icon: faRectangleList },
		{ href: '/education', name: 'Education', icon: faGraduationCap },
		{ href: '/design', name: 'Design', icon: faPaintbrush },
		{ href: '/keys', name: 'Keys', icon: faKey }
	];
	let iconLinks = {
		email: 'mailto:contact@brianlu.me',
		linkedin: 'https://www.linkedin.com/in/greencappuccino/',
		github: 'https://github.com/GreenCappuccino'
	};
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
	<div
		class="mb-10 mt-5 mx-5 ml-auto flex flex-row items-center gap-5 sm:gap-3 text-gray-700 dark:text-gray-400"
	>
		<a id="email-icon" href={iconLinks.email}>
			<Icon data={faEnvelope} style="width: 2em; height: 2em" />
		</a>
		<a id="linkedin-icon" href={iconLinks.linkedin}>
			<Icon data={faLinkedin} style="width: 2em; height: 2em" />
		</a>
		<a id="github-icon" href={iconLinks.github}>
			<Icon data={faGithub} style="width: 2em; height: 2em" />
		</a>
		<Popover
			class="w-48 text-sm font-normal text-gray-700 dark:text-gray-400 "
			placement="bottom"
			title="Contact Email"
			triggeredBy="#email-icon"
		>
			<a href={iconLinks.email}>
				<p class="underline">contact@brianlu.me</p>
			</a>
		</Popover>
		<Popover
			class="w-48 text-sm font-normal text-gray-700 dark:text-gray-400 "
			placement="bottom"
			title="Linkedin Profile"
			triggeredBy="#linkedin-icon"
		>
			<a href={iconLinks.linkedin}>
				<p class="underline">in/greencappuccino</p>
			</a>
		</Popover>
		<Popover
			class="w-48 text-sm font-normal text-gray-700 dark:text-gray-400 "
			placement="bottom"
			title="Github Profile"
			triggeredBy="#github-icon"
		>
			<a href={iconLinks.github}>
				<p class="underline">GreenCappuccino</p>
			</a>
		</Popover>
	</div>
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
		Practical Chaos at Scale
	</Heading>
	<ButtonGroup class="mb-4 justify-center items-center hidden sm:flex">
		{#each links as link}
			<Button href={link.href}>
				{#if link.icon}
					<Icon data={link.icon} class="mr-2" width="1em" height="1em" />
				{/if}
				{link.name}
			</Button>
		{/each}
		<DarkMode />
	</ButtonGroup>
	<div class="mb-4 ml-2 mr-2 flex flex-row flex-wrap justify-center space-x-2 sm:hidden">
		<Button class="mt-1 mb-1" color="alternative" on:click={() => (hideDrawer = false)}>
			<Icon data={faBars} class="mr-2" width="1em" height="1em" />
			Menu
		</Button>
		<Button class="mt-1 mb-1" color="alternative" href="/">
			<Icon data={faHouseChimney} class="mr-2" width="1em" height="1em" />
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
							<Icon data={link.icon} slot="icon" />
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

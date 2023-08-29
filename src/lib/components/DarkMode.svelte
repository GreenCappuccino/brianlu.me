<script lang="ts">
	import { Button } from 'flowbite-svelte';
	import { faMoon, faSun } from '@fortawesome/free-solid-svg-icons';
	import { Icon } from 'svelte-awesome';

	export let buttonClass = '';

	// Default DarkMode component is not playing nice with other Button components style-wise
	const toggleTheme = () => {
		const isDark = window.document.documentElement.classList.toggle('dark');
		localStorage.setItem('color-theme', isDark ? 'dark' : 'light');
	};
</script>

<Button class={buttonClass} color="alternative" on:click={toggleTheme}>
	<Icon data={faMoon} class="!hidden dark:!block w-[20px] h-[20px]" />
	<Icon data={faSun} class="!block dark:!hidden w-[20px] h-[20px]" />
</Button>

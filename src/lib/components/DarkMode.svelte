<script lang="ts">
	import { Button } from 'flowbite-svelte';
	import * as Icon from 'svelte-awesome-icons';

	export let buttonClass = '';

	// Default DarkMode component is not playing nice with other Button components style-wise
	const toggleTheme = () => {
		const isDark = window.document.documentElement.classList.toggle('dark');
		localStorage.setItem('color-theme', isDark ? 'dark' : 'light');
	};
</script>

<Button class={buttonClass} color="alternative" on:click={toggleTheme}>
	<Icon.MoonSolid size="3ex" class="hidden dark:block" />
	<Icon.SunSolid size="3ex" class="dark:hidden" />
</Button>

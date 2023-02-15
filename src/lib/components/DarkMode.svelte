<script lang="ts">
	import { Button } from 'flowbite-svelte';
	import { MoonSolid, SunSolid } from 'svelte-awesome-icons';

	export let buttonClass = '';

	// Default DarkMode component is not playing nice with other Button components style-wise
	const toggleTheme = () => {
		const isDark = window.document.documentElement.classList.toggle('dark');
		localStorage.setItem('color-theme', isDark ? 'dark' : 'light');
	};
</script>

<Button class={buttonClass} color="alternative" on:click={toggleTheme}>
	<MoonSolid class="hidden dark:block" size="3ex" />
	<SunSolid class="dark:hidden" size="3ex" />
</Button>

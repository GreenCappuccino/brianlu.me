<script lang="ts">
	import { Card, Img } from 'flowbite-svelte';
	import { GithubBrand } from 'svelte-awesome-icons';

	let items = [
		{
			title: 'cat',
			description:
				'pspsp spspspspspspspsp spspspspspspspspspsps pspspspspspsp spspspsps pspspsps&nbsp;&raquo;',
			img: 'https://purr.objects-us-east-1.dream.io/i/bgnBP.jpg',
			href: 'http://random.cat/view/691',
			github: {
				p: 'placeholder'
			}
		}
	];
</script>

<svelte:head>
	<title>Projects | Brian Lu</title>
</svelte:head>

{#each items as item, itemIndex}
	<Card img={item.img} href={item.href} horizontal>
		<div class="flex flex-row items-start">
			<div class="mr-auto">
				{#if item.headImg}
					<Img
						src={item.headImg}
						size="w-96 h-fit"
						alignment="mb-2"
						class={item.headImgDark ? 'dark:hidden' : null}
						alt={item.headImgAlt}
					/>
				{/if}
				{#if item.headImgDark}
					<Img
						src={item.headImgDark}
						size="w-96 h-fit"
						alignment="mb-2"
						class="hidden dark:block"
						alt={item.headImgAlt}
					/>
				{/if}
				{#if item.title && !item.hideTitle}
					<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
						{item.title}
					</h5>
				{/if}
			</div>
			{#if item.github}
				<GithubBrand />
			{/if}
		</div>
		{#if item.description}
			<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
				{@html item.description}
			</p>
		{/if}
	</Card>
	{#if itemIndex < items.length - 1}
		<div class="m-2" />
	{/if}
{/each}

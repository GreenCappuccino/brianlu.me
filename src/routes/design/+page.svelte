<script lang="ts">
	import { Card, Img } from 'flowbite-svelte';

	let items = [
		{
			title: 'Shamrock Systems',
			hideTitle: true,
			description:
				'The Shamrock compute cluster comes equipped with its own design language. See how it looks and behaves here&nbsp;&raquo;',
			img: '/images/ShamrockDesignSquareThumb.png',
			headImg: '/images/shamrock-light.png',
			headImgDark: '/images/shamrock-dark.png',
			headImgAlt: 'The Shamrock Logo',
			href: '/design/shamrock'
		},
		{
			title: 'Crucible SDS',
			hideTitle: true,
			description:
				'The Crucible SDS data processing suite I worked on has a series of logos for each of its software components. Combined they have a unified style&nbsp;&raquo;',
			img: '/images/cruciblesquare.png',
			headImg: '/images/crucible-wide-light.png',
			headImgDark: '/images/crucible-wide-dark.png',
			headImgAlt: 'The Crucible Logo',
			href: '/design/crucible'
		},
	];
</script>

<svelte:head>
	<title>Design | Brian Lu</title>
</svelte:head>

{#each items as item, itemIndex}
	<Card img={item.img} href={item.href} horizontal>
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

<script>
	import { Img, Timeline, TimelineItem } from 'flowbite-svelte';
	import * as Icon from 'svelte-awesome-icons';

	let items = [
		{
			name: 'Purdue University',
			date: 'August 2022',
			img: '/images/Purdue_Boilermakers_logo.svg.png',
			imgAlt: 'Purdue Boilermakers Motion P Logo',
			desc: 'Test decription please ignore',
		},
		{
			name: 'Naperville Central High School',
			date: 'August 2018 - May 2022',
			img: '/images/NapervilleCentHSlogo.png',
			imgAlt: 'Naperville Central High School Logo',
			desc: 'Test decription please ignore',
		}
	];
</script>

<Timeline order="vertical">
	{#each items as item}
		<div class="flex flex-row">
			<TimelineItem title={item.name} date={item.date}>
				<svelte:fragment slot="icon">
					<span
						class="flex absolute -left-3 justify-center items-center w-6 h-6 bg-blue-200 rounded-full ring-8 ring-white dark:ring-gray-800 dark:bg-blue-900"
					>
						<Icon.CalendarSolid size="0.75em" />
					</span>
				</svelte:fragment>
				{#if item.desc}
					<p class="mb-4 text-base font-normal text-gray-500 dark:text-gray-400">
						{item.desc}
					</p>
				{/if}
			</TimelineItem>
			{#if item.img}
				<Img src={item.img} size="w-12 h-fit" alignment="ml-auto pl-5 mt-2" alt={item.imgAlt} />
			{/if}
		</div>
	{/each}
</Timeline>

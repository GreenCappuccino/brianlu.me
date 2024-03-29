<script lang="ts">
	import { Badge, Img, Timeline, TimelineItem } from 'flowbite-svelte';
	import {
		faBuildingColumns,
		faCalculator,
		faCircleNodes,
		faCodeMerge,
		faComputer,
		faDiagramProject,
		faFileWaveform,
		faMicrochip,
		faSchool,
		faWaveSquare
	} from '@fortawesome/free-solid-svg-icons';
	import { Icon } from 'svelte-awesome';
	import { faPython } from '@fortawesome/free-brands-svg-icons';

	let items = [
		{
			name: 'Purdue University',
			date: 'August 2022 - May 2025',
			img: '/images/Purdue_Boilermakers_logo.svg.png',
			imgAlt: 'Purdue Boilermakers Motion P Logo',
			timelineIcon: faBuildingColumns,
			shortDesc: 'B.S. in Computer Engineering',
			notables: [
				{ course: 'ECE 30100 - Signals and Systems', icon: faFileWaveform, ongoing: true },
				{ course: 'ECE 20875 - Python for Data Science', icon: faPython, ongoing: true },
				{ course: 'ECE 27000 - Introduction To Digital Design', icon: faWaveSquare },
				{ course: 'ECE 33700 - ASIC Design Lab', icon: faMicrochip, ongoing: true },
				{ course: 'ECE 20001 - Electrical Engineering Fundamentals I', icon: faFileWaveform },
				{ course: 'ECE 20002 - Electrical Engineering Fundamentals II', icon: faFileWaveform },
				{ course: 'ECE 36800 - Data Structures', icon: faCircleNodes, ongoing: true },
				{ course: 'ECE 26400 - Advanced C Programming', icon: faComputer },
				{ course: 'ECE 36900 - Discrete Math', icon: faDiagramProject },
				{ course: 'MA 26600 - Differential Equations', icon: faCalculator }
			],
			ongoing: true
		},
		{
			name: 'College of DuPage',
			date: 'May 2022 - August 2022',
			img: '/images/COD_Logo.svg',
			imgAlt: 'College of DuPage Logo',
			timelineIcon: faBuildingColumns,
			notables: [{ course: 'MATH 2245 - Linear Algebra', icon: faCalculator }]
		},
		{
			name: 'Naperville Central High School',
			date: 'August 2018 - May 2022',
			img: '/images/NapervilleCentHSlogo.png',
			imgAlt: 'Naperville Central High School Logo',
			timelineIcon: faSchool,
			shortDesc: 'High School Diploma',
			notables: [
				{ course: 'AP Calculus BC', icon: faCalculator },
				{ course: 'UIUC MA 241 - Calculus 3', icon: faCalculator },
				{ course: 'Software Engineering', icon: faCodeMerge }
			]
		}
	];
</script>

<svelte:head>
	<title>Education | Brian Lu</title>
</svelte:head>

<div class="ml-1 sm:ml-0">
	<Timeline order="vertical">
		{#each items as item}
			<div class="flex flex-row items-start">
				<TimelineItem title={item.name} date={item.date}>
					<svelte:fragment slot="icon">
						<span
							class="flex absolute -left-3 justify-center items-center w-6 h-6 bg-blue-200 rounded-full ring-8 ring-white dark:ring-gray-800 dark:bg-blue-900"
						>
							<Icon data={item.timelineIcon} width="0.75em" height="0.75em" />
						</span>
					</svelte:fragment>
					{#if item.shortDesc}
						<div class="flex flex-row items-center mb-2">
							<p class="text-base font-bold text-gray-500 dark:text-gray-400">
								{item.shortDesc}
							</p>
							{#if item.ongoing}
								<Badge color="green" class="ml-2">Ongoing</Badge>
							{/if}
						</div>
					{/if}
					{#if item.notables}
						<p class="mb-1 text-base font-normal text-gray-500 dark:text-gray-400">
							Notable coursework:
						</p>
						<ul class="dark:text-gray-400">
							{#each item.notables as notable, notableIndex}
								<li>
									<div class="flex flex-row items-center">
										<Icon data={notable.icon} width="1em" height="1em" class="mr-2" />
										<p>{notable.course}</p>
										{#if notable.ongoing}
											<div class="ml-auto flex flex-row items-center">
												<Badge color="green" class="ml-2">Ongoing</Badge>
											</div>
										{/if}
									</div>
									{#if notableIndex < item.notables.length - 1}
										<hr class="border-gray-200 dark:border-gray-700 mt-1 mb-1" />
									{/if}
								</li>
							{/each}
						</ul>
					{/if}
				</TimelineItem>
				{#if item.img}
					<Img src={item.img} size="w-12 h-auto" alignment="ml-auto pl-5 mt-2" alt={item.imgAlt} />
				{/if}
			</div>
		{/each}
	</Timeline>
</div>

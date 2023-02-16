<script lang="ts">
	import { Badge, Img, Timeline, TimelineItem } from 'flowbite-svelte';
	import {
		BuildingColumnsSolid,
		CalculatorSolid,
		CodeMergeSolid,
		ComputerSolid,
		DiagramProjectSolid,
		FileWaveformSolid,
		MicrochipSolid,
		SchoolSolid,
		WaveSquareSolid
	} from 'svelte-awesome-icons';

	let items = [
		{
			name: 'Purdue University',
			date: 'August 2022 - Present',
			img: '/images/Purdue_Boilermakers_logo.svg.png',
			imgAlt: 'Purdue Boilermakers Motion P Logo',
			timelineIcon: BuildingColumnsSolid,
			shortDesc: 'B.S. in Computer Engineering',
			notables: [
				{ course: 'ECE 27000 - Introduction To Digital Design', icon: WaveSquareSolid },
				{ course: 'ECE 33700 - ASIC Design Lab', icon: MicrochipSolid, ongoing: true },
				{ course: 'ECE 20001 - Electrical Engineering Fundamentals I', icon: FileWaveformSolid },
				{
					course: 'ECE 20002 - Electrical Engineering Fundamentals II',
					icon: FileWaveformSolid,
					ongoing: true
				},
				{ course: 'ECE 26400 - Advanced C Programming', icon: ComputerSolid, ongoing: true },
				{ course: 'ECE 36900 - Discrete Math', icon: DiagramProjectSolid, ongoing: true },
				{ course: 'MA 26600 - Differential Equations', icon: CalculatorSolid }
			],
			ongoing: true
		},
		{
			name: 'College of DuPage',
			date: 'May 2022 - August 2022',
			img: '/images/COD_Logo.svg',
			imgAlt: 'College of DuPage Logo',
			timelineIcon: BuildingColumnsSolid,
			notables: [{ course: 'MATH 2245 - Linear Algebra', icon: CalculatorSolid }]
		},
		{
			name: 'Naperville Central High School',
			date: 'August 2018 - May 2022',
			img: '/images/NapervilleCentHSlogo.png',
			imgAlt: 'Naperville Central High School Logo',
			timelineIcon: SchoolSolid,
			shortDesc: 'High School Diploma',
			notables: [
				{ course: 'AP Calculus BC', icon: CalculatorSolid },
				{ course: 'UIUC MA 241 - Calculus 3', icon: CalculatorSolid },
				{ course: 'Software Engineering', icon: CodeMergeSolid }
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
			<div class="flex flex-row">
				<TimelineItem title={item.name} date={item.date}>
					<svelte:fragment slot="icon">
						<span
							class="flex absolute -left-3 justify-center items-center w-6 h-6 bg-blue-200 rounded-full ring-8 ring-white dark:ring-gray-800 dark:bg-blue-900"
						>
							<svelte:component this={item.timelineIcon} size="0.75em" />
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
										<svelte:component this={notable.icon} size="1em" class="mr-2" />
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
					<Img src={item.img} size="w-12 h-fit" alignment="ml-auto pl-5 mt-2" alt={item.imgAlt} />
				{/if}
			</div>
		{/each}
	</Timeline>
</div>

<script>
	import { Badge, Card, Img, Timeline, TimelineItem } from 'flowbite-svelte';
	import {
		BoltSolid,
		BriefcaseSolid,
		ChalkboardUserSolid,
		DiagramProjectSolid,
		DownloadSolid,
		EyeSolid,
		FileSolid,
		GearSolid,
		PrintSolid,
		ServerSolid
	} from 'svelte-awesome-icons';

	let experiences = [
		{
			title: 'Merck Sharp & Dohme',
			date: '2022 - Present',
			img: '/images/MerckColor.svg',
			imgDark: '/images/MerckWhite.svg',
			imgAlt: 'Merck Logo',
			timelineIcon: BriefcaseSolid,
			shortDesc: 'Student Researcher',
			points: [
				{
					text: 'Architected Safety Data Sheet (SDS) parsing and insights software with team',
					icon: DiagramProjectSolid
				},
				{
					text: 'Software cuts down on hours of work per day reading SDS documents, is currently being integrated',
					icon: ServerSolid
				},
				{
					text: 'Wrote low-level PDF parsing engine to extract document hierarchies, fields, and images',
					icon: FileSolid
				},
				{
					text: 'Created OpenCV-based classifier to accurately detect GHS pictograms',
					icon: EyeSolid
				},
				{
					text: 'Developed automated PDF templating pipeline to create reports of generated insights',
					icon: PrintSolid
				}
			],
			ongoing: true
		},
		{
			title: 'High Oak Robotics',
			date: '2021 - 2023',
			img: '/images/highoak.png',
			imgAlt: 'High Oak Robotics Logo',
			timelineIcon: BriefcaseSolid,
			shortDesc: 'Robotics Coach',
			points: [
				{
					text: 'Wrote and maintained <a href="/projects" class="text-blue-500">Sequoia</a> asynchronous scheduling library',
					icon: GearSolid
				},
				{
					text: 'Teaching of robotics control system concepts to new team members',
					icon: ChalkboardUserSolid
				},
				{ text: 'Bootstrapped sensor fusion and navigation technology stack', icon: BoltSolid }
			]
		}
	];

	let pageCards = [
		{
			title: 'Projects',
			href: '/projects',
			img: '/images/projects.png',
			description: 'Software, Hardware, Hackathons&nbsp;&raquo;'
		},
		{
			title: 'Education',
			href: '/education',
			img: '/images/education.png',
			description: 'High School and University&nbsp;&raquo;'
		},
		{
			title: 'Design',
			href: '/design',
			img: '/images/ShamrockDesignSquareThumb.png',
			description: 'Just for fun&nbsp;&raquo;'
		},
		{
			title: 'Keys',
			href: '/keys',
			img: '/images/encryption.jpg',
			description: 'Public key cryptography&nbsp;&raquo;'
		}
	];
</script>

<svelte:head>
	<title>Home | Brian Lu</title>
</svelte:head>

<div class="max-w-full mb-2">
	<div class="mb-4 flex flex-row items-center">
		<h3 class="text-4xl font-bold text-gray-900 dark:text-white leading-tight">Hello!</h3>
		<a href="/doc/Resume.pdf" class="ml-auto flex flex-row items-end">
			<p class="text-right">Download Resume</p>
			<DownloadSolid class="ml-2" />
		</a>
	</div>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		I'm a <b>Computer Engineering</b> student at <b>Purdue University Main Campus</b>.
	</p>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		In the past I wrote and maintained <b>navigation</b> and <b>scheduling</b> software for competitive
		robotics.
	</p>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		Now, I'm working on quickly and accurately <b>parsing</b> and structuring <b>1,000s</b> of chemical
		Safety Data Sheet PDFs for Merck.
	</p>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		I have a passion for homelabbing, and own and operate the <a
			href="https://shamrock.systems"
			class="text-blue-500">Shamrock Cluster</a
		>.
	</p>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		It tries to be as production-ready as possible by leveraging <b>high-availability</b>
		technologies, filesystem
		<b>encryption</b>, and ensuring <b>mutual TLS</b> authentication every step of the way.
	</p>
</div>

<!--It's template-land from here on out.-->
<h4 class="mb-4 text-3xl font-bold tracking-tight text-gray-900 dark:text-white">Experience</h4>
<div class="ml-1 sm:ml-0">
	<Timeline order="vertical">
		{#each experiences as experience}
			<div class="flex flex-row items-start">
				<TimelineItem title={experience.title} date={experience.date}>
					<svelte:fragment slot="icon">
						<span
							class="flex absolute -left-3 justify-center items-center w-6 h-6 bg-blue-200 rounded-full ring-8 ring-white dark:ring-gray-800 dark:bg-blue-900"
						>
							<svelte:component this={experience.timelineIcon} size="0.75em" />
						</span>
					</svelte:fragment>
					<div class="flex flex-row items-center mb-2">
						<p class="text-base font-bold text-gray-500 dark:text-gray-400">
							{experience.shortDesc}
						</p>
						{#if experience.ongoing}
							<Badge color="green" class="ml-2">Ongoing</Badge>
						{/if}
					</div>
					<ul class="dark:text-gray-400">
						{#each experience.points as point, pointIndex}
							<li>
								<div class="flex flex-row items-center">
									<svelte:component this={point.icon} size="1em" class="mr-2" />
									<p>{@html point.text}</p>
								</div>
							</li>
							{#if pointIndex < experience.points.length - 1}
								<hr class="border-gray-200 dark:border-gray-700 mt-1 mb-1" />
							{/if}
						{/each}
					</ul>
				</TimelineItem>
				{#if experience.img}
					<Img
						src={experience.img}
						size="w-12 h-auto"
						alignment="ml-auto pl-5 mt-2"
						class={experience.imgDark ? 'dark:hidden' : ''}
						alt={experience.imgAlt}
					/>
					{#if experience.imgDark}
						<Img
							src="/images/MerckWhite.svg"
							size="w-12 h-auto"
							alignment="ml-auto pl-5 mt-2"
							class="hidden dark:block"
							alt={experience.imgAlt}
						/>
					{/if}
				{/if}
			</div>
		{/each}
	</Timeline>
</div>
<div class="mt-4 grid grid-cols-1 self-center sm:grid-cols-2 gap-4">
	{#each pageCards as pageCard}
		<Card img={pageCard.img} href={pageCard.href}>
			<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
				{pageCard.title}
			</h5>
			{#if pageCard.description}
				<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
					{@html pageCard.description}
				</p>
			{/if}
		</Card>
	{/each}
</div>

<script lang="ts">
	import { Badge, Card } from 'flowbite-svelte';
	import { faChevronRight, faKey } from '@fortawesome/free-solid-svg-icons';
	import { Icon } from 'svelte-awesome';

	let items = [
		{
			name: 'GPG',
			href: 'keys/gpg/all',
			keys: [
				{
					name: 'Primary',
					href: '/keys/gpg/primary',
					email: 'me@greencappuccino.net',
					key: 'A96D4D81BF36A735',
					subKeys: ['D3A2F1D6D494782F']
				}
			]
		},
		{
			name: 'SSH',
			href: '/keys/ssh/all',
			keys: [
				{
					name: 'RSA',
					hash: 'SHA256:sKN3gqkdMbX+wRKzgNKtH32uftcQR5vlKQ94EhUNVDs',
					href: '/keys/ssh/rsa'
				},
				{
					name: 'ED25519',
					hash: 'SHA256:DbxwKAU9wFh0VhKKrTi4eLrDahWAHP9fDWFKeTZ5wnM',
					href: '/keys/ssh/ed25519'
				}
			]
		}
	];
</script>

<svelte:head>
	<title>Keys | Brian Lu</title>
</svelte:head>

<div class="max-w-sm md:max-w-xl mb-2">
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		If you want to verify my commits, authenticate me, etc, here are my GPG and SSH keys.
	</p>
	<p class="mb-3 font-normal text-gray-700 dark:text-gray-400 leading-tight">
		If you're not looking for these, it's probably not important for you right now.
	</p>
</div>
{#each items as item, itemIndex}
	<div class="flex flex-row items-baseline">
		<h4 class="mb-2 text-3xl font-bold tracking-tight text-gray-900 dark:text-white">
			{item.name}
		</h4>
		{#if item.href}
			<a href={item.href} class="ml-2 flex flex-row items-center">
				<p class="text-l font-bold">All</p>
				<Icon data={faChevronRight} width="1em" height="1em" />
			</a>
		{/if}
	</div>
	{#each item.keys as key, keyIndex}
		<Card
			horizontal
			href={key.href}
			class={itemIndex < items.length - 1 || keyIndex < item.keys.length - 1 ? 'mb-4' : ''}
		>
			<div class="flex flex-row w-full">
				<div class="mt-auto mb-auto mr-4">
					<Icon data={faKey} width="24" height="24" />
				</div>
				<div>
					<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
						{key.name}
					</h5>
					{#if key.hash}<p class="font-mono break-all">{key.hash}</p>{/if}
					{#if key.key}
						<div class="flex flex-wrap mb-2">
							<p>Key:</p>
							<Badge color="green" class="font-mono break-all ml-2">{key.key}</Badge>
						</div>
					{/if}
					{#if key.subKeys}
						<div class="flex flex-wrap mb-2">
							<p>Subkeys:</p>
							{#each key.subKeys as subKey}
								<Badge class="font-mono break-all ml-2">{subKey}</Badge>
							{/each}
						</div>
					{/if}
				</div>
				<Icon data={faChevronRight} class="mt-auto mb-auto ml-auto pl-4 w-[2em] h-[2em]" />
			</div>
		</Card>
	{/each}
{/each}

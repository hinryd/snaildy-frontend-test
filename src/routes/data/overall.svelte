<script lang="ts">
	import { DownloadIcon, UserIcon } from '@rgossiaux/svelte-heroicons/outline';

	let data = [
		{
			region: {
				name: 'France',
				code: 'FR',
				districts: [
					{
						name: 'Paris',
						code: '75',
						cities: []
					}
				]
			},
			lastInput: 100000,
			formCount: 1000,
			voterCount: 100000,
			update: 345678
		}
	];
</script>

<tbody>
	{#each data as dataPoint}
		<tr class="divide-x-1 divide-black text-center">
			<td class="p-4 flex">
				<div class="flex items-center gap-2 flex-grow flex-shrink-0">
					<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">
						<UserIcon />
					</div>
					<p>Hong Kong</p>
					<button class="h-6 w-6 bg-green-400 rounded p-1"><DownloadIcon /></button>
				</div>
				<button class="rounded bg-gray-200 p-1"
					>{dataPoint.region.districts.length} districts</button
				>
			</td>
			<td>{dataPoint.lastInput}</td>
			<td>{dataPoint.formCount}</td>
			<td>{dataPoint.voterCount}</td>
			<td>{dataPoint.update}</td>
		</tr>
	{/each}
</tbody>

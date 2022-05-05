<script lang="ts">
	import {
		ChevronDoubleRightIcon,
		ChevronRightIcon,
		DownloadIcon,
		UserIcon
	} from '@rgossiaux/svelte-heroicons/outline';

	let data = [
		{
			id: 0,
			region: {
				name: 'France',
				code: 'FR',
				districts: [
					{
						name: 'Paris',
						code: '75',
						cities: [
							{
								name: 'Paris',
								code: '75001',
								lastInput: 100000,
								formCount: 1000,
								voterCount: 100000,
								update: 345678
							}
						],
						lastInput: 100000,
						formCount: 1000,
						voterCount: 100000,
						update: 345678
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
	{#each data as dataPoint (dataPoint.id)}
		<tr class="divide-x-1 divide-black text-center">
			<td class="p-4 flex">
				<div class="flex items-center gap-2 flex-grow flex-shrink-0">
					<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">
						<UserIcon />
					</div>
					<p>{dataPoint.region.name}</p>
					<button class="h-6 w-6 bg-green-400 rounded p-1"><DownloadIcon /></button>
				</div>
				<button class="rounded bg-gray-200 p-1 flex-shrink-0"
					>{dataPoint.region.districts.length} districts</button
				>
			</td>
			<td>{dataPoint.lastInput}</td>
			<td>{dataPoint.formCount}</td>
			<td>{dataPoint.voterCount}</td>
			<td>{dataPoint.update}</td>
		</tr>
		{#each dataPoint.region.districts as district}
			<tr class="divide-x-1 divide-black text-center">
				<td class="p-4 flex">
					<div class="flex items-center gap-2 flex-grow flex-shrink-0">
						<div class="h-3 w-3">
							<ChevronRightIcon />
						</div>
						<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">
							<UserIcon />
						</div>
						<p>{district.name}</p>
						<button class="h-6 w-6 bg-green-400 rounded p-1"><DownloadIcon /></button>
					</div>
					<button class="rounded bg-gray-200 p-1 flex-shrink-0"
						>{district.cities.length}
						<span class="hidden sm:inline">cities</span></button
					>
				</td>
				<td>{district.lastInput}</td>
				<td>{district.formCount}</td>
				<td>{district.voterCount}</td>
				<td>{district.update}</td>
			</tr>
			{#each district.cities as city}
				<tr class="divide-x-1 divide-black text-center">
					<td class="p-4 flex">
						<div class="flex items-center gap-2 flex-grow flex-shrink-0">
							<div class="w-1" />
							<div class="h-3 w-3">
								<ChevronDoubleRightIcon />
							</div>
							<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">
								<UserIcon />
							</div>
							<p>{city.name}</p>
							<button class="h-6 w-6 bg-green-400 rounded p-1"><DownloadIcon /></button>
						</div>
					</td>
					<td>{city.lastInput}</td>
					<td>{city.formCount}</td>
					<td>{city.voterCount}</td>
					<td>{city.update}</td>
				</tr>
			{/each}
		{/each}
	{/each}
</tbody>

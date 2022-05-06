<script lang="ts">
	import {
		Listbox,
		ListboxButton,
		ListboxOptions,
		ListboxOption
	} from '@rgossiaux/svelte-headlessui';
	import {
		SearchIcon,
		ChevronDownIcon,
		DotsHorizontalIcon,
		DownloadIcon,
		MinusIcon,
		PlusIcon,
		UserIcon
	} from '@rgossiaux/svelte-heroicons/outline';

	const filters = ['Filter', 'Active', 'Inactive'];
	let selectedFilter = filters[0];
	let searchText = '';
	const data = [
		{
			region: {
				name: 'Hong Kong',
				showDistricts: false,
				districts: [
					{
						name: 'Central',
						showCities: false,
						cities: [
							{
								name: 'Central',
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
					},
					{
						name: 'Eastern',
						showCities: false,
						cities: [
							{
								name: 'Eastern',
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
		},
		{
			region: {
				name: 'France',
				showDistricts: false,
				districts: [
					{
						name: 'Paris',
						showCities: false,
						cities: [
							{
								name: 'Paris',
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
	let filteredData = data;
</script>

<main class="h-screen w-screen bg-indigo-300 p-2 sm:p-8 transition-all duration-75 overflow-x-auto">
	<div class="bg-white rounded shadow-md ">
		<form
			class="h-14 flex items-stretch divide-x divide-gray-300 border-b border-gray-300 text-sm sm:text-base"
			on:submit|preventDefault={() =>
				(filteredData = data.filter((item) =>
					item.region.name.toLowerCase().includes(searchText.toLowerCase())
				))}
		>
			<div class="w-25 m-1 p-2 flex items-center">
				<Listbox
					class="relative"
					value={selectedFilter}
					on:change={(e) => (selectedFilter = e.detail)}
				>
					<ListboxButton class="flex items-center justify-between w-28">
						<span class:text-gray-300={selectedFilter === filters[0]}>{selectedFilter}</span>
						<div class="h-4 w-4 text-black"><ChevronDownIcon /></div>
					</ListboxButton>
					<ListboxOptions class="absolute bg-white shadow-md rounded w-28">
						{#each filters as filter}
							<ListboxOption class="p-4" value={filter}>
								<span class:text-gray-300={filter === filters[0]}>{filter}</span>
							</ListboxOption>
						{/each}
					</ListboxOptions>
				</Listbox>
			</div>
			<div class="flex justify-between w-full">
				<input class="p-2 w-full" type="text" placeholder="Search" bind:value={searchText} />
				<button class="p-4" type="submit"><SearchIcon class="h-6 w-6" /></button>
			</div>
		</form>

		<div class="overflow-x-scroll">
			<table class="text-xs w-full">
				<thead>
					<tr class="border-b-2 border-black divide-x divide-gray-300">
						<th class="p-3 font-light">Region</th>
						<th class="p-3 font-light">Last input</th>
						<th class="p-3 font-light">Number of forms</th>
						<th class="p-3 font-light">Number of voters</th>
						<th class="p-3 font-light">Update</th>
					</tr>
				</thead>
				<tbody class="divide-y divide-gray-300">
					{#each filteredData as dataPoint}
						<tr class="divide-x divide-gray-300 text-center">
							<td class="py-2 px-4 flex justify-between gap-3">
								<div class="flex items-center gap-3 flex-shrink-0">
									<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">S</div>
									<p class="whitespace-nowrap">{dataPoint.region.name}</p>
									<button class="h-6 w-6 bg-green-400 rounded p-1 text-white"
										><DownloadIcon /></button
									>
								</div>
								<button
									class="rounded p-1 flex items-center gap-1 flex-shrink-0 {dataPoint.region
										.showDistricts
										? 'bg-gray-300'
										: 'bg-gray-200'}"
									on:click|preventDefault={() =>
										(dataPoint.region.showDistricts = !dataPoint.region.showDistricts)}
								>
									{dataPoint.region.districts.length}
									<span class="hidden sm:inline"
										>district{dataPoint.region.districts.length !== 1 ? 's' : ''}</span
									>
									{#if !dataPoint.region.showDistricts}
										<PlusIcon class="h-3 w-3" />
									{:else}
										<MinusIcon class="h-3 w-3" />
									{/if}
								</button>
							</td>
							<td>{dataPoint.lastInput}</td>
							<td>{dataPoint.formCount}</td>
							<td>{dataPoint.voterCount}</td>
							<td>{dataPoint.update}</td>
						</tr>
						{#if dataPoint.region.showDistricts}
							{#each dataPoint.region.districts as district}
								<tr class="text-center divide-x divide-gray-300">
									<td class="py-2 px-4 flex justify-between gap-3">
										<div class="flex items-center gap-3 flex-shrink-0">
											<DotsHorizontalIcon class="h-4 w-4 ml-2" />
											<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">D</div>
											<p class="whitespace-nowrap">{district.name}</p>
											<button class="h-6 w-6 bg-green-400 rounded p-1 text-white"
												><DownloadIcon /></button
											>
										</div>
										<button
											class="rounded p-1 flex items-center gap-1 flex-shrink-0 {district.showCities
												? 'bg-gray-300'
												: 'bg-gray-200'}"
											on:click|preventDefault={() => (district.showCities = !district.showCities)}
										>
											{district.cities.length}
											<span class="hidden sm:inline"
												>township{district.cities.length !== 1 ? 's' : ''}</span
											>
											{#if !district.showCities}
												<PlusIcon class="h-3 w-3" />
											{:else}
												<MinusIcon class="h-3 w-3" />
											{/if}
										</button>
									</td>
									<td>{district.lastInput}</td>
									<td>{district.formCount}</td>
									<td>{district.voterCount}</td>
									<td>{district.update}</td>
								</tr>
								{#if district.showCities}
									{#each district.cities as city}
										<tr class="text-center divide-x divide-gray-300">
											<td class="py-2 px-4 flex justify-between gap-3">
												<div class="flex items-center gap-3 flex-grow flex-shrink-0">
													<DotsHorizontalIcon class="h-4 w-4 ml-11" />
													<div class="h-6 w-6 bg-indigo-400 rounded-full p-1 text-white">T</div>
													<p class="whitespace-nowrap">{city.name}</p>
													<button class="h-6 w-6 bg-green-400 rounded p-1 text-white"
														><DownloadIcon /></button
													>
												</div>
											</td>
											<td>{city.lastInput}</td>
											<td>{city.formCount}</td>
											<td>{city.voterCount}</td>
											<td>{city.update}</td>
										</tr>
									{/each}
								{/if}
							{/each}
						{/if}
					{/each}
				</tbody>
			</table>
		</div>
	</div>
</main>

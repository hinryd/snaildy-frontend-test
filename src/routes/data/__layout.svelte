<script lang="ts">
	import { SearchIcon, ChevronDownIcon } from '@rgossiaux/svelte-heroicons/outline';
	import {
		Listbox,
		ListboxButton,
		ListboxOptions,
		ListboxOption
	} from '@rgossiaux/svelte-headlessui';

	const filters = ['Filter', 'Active', 'Inactive'];
	let selectedFilter = filters[0];
</script>

<main class="h-screen w-screen bg-indigo-300 p-2 sm:p-8 transition-all duration-75 overflow-x-auto">
	<div class="bg-white rounded shadow-md">
		<form class="h-14 flex items-stretch divide-x divide-gray-300 border-b border-gray-300">
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
					<ListboxOptions class="absolute bg-white shadow-md rounded">
						{#each filters as filter}
							<ListboxOption class="p-4" value={filter}>
								<span class:text-gray-300={filter === filters[0]}>{filter}</span>
							</ListboxOption>
						{/each}
					</ListboxOptions>
				</Listbox>
			</div>
			<div class="flex justify-between w-full">
				<input class="p-2 flex-grow" type="text" placeholder="Search" />
				<button class="p-4" type="submit"> <div class="h-6 w-6"><SearchIcon /></div></button>
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
				<slot />
			</table>
		</div>
	</div>
</main>

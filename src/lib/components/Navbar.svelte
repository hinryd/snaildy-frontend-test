<script lang="ts">
	import { page } from '$app/stores';
	import { HomeIcon } from '@rgossiaux/svelte-heroicons/outline';
</script>

<nav
	class="sticky top-0 bg-white h-14 w-screen shadow-md grid grid-cols-12 divide-x divide-gray-300 text-xs sm:text-base"
>
	<div class="col-span-8 flex items-stretch divide-x divide-gray-300">
		<a class="p-4" href="/">
			<div class="h-6 w-6"><HomeIcon /></div>
		</a>
		<h1 class="px-4 flex items-center font-bold">Reports</h1>
	</div>
	<a
		class="col-span-2 flex items-center justify-center"
		class:bg-indigo-100={$page.url.searchParams.get('type') === 'overall'}
		href="/records?type=overall">Overall</a
	>
	<a
		class="col-span-2 flex items-center justify-center"
		class:bg-indigo-100={$page.url.searchParams.get('type') === 'specific'}
		href="/records?type=specific">Specific</a
	>
</nav>

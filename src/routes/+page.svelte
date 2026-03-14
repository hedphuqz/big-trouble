<script lang="ts">
	import logo from '$lib/assets/big-trouble.svg';
	import List from '$lib/components/List.svelte';
	import TextInput from '$lib/components/TextInput.svelte';
	import bigFishTrouble from '$lib/assets/big-fish-trouble.jpeg';
	const shows = [
		{ date: '15.03', label: 'Berlin' },
		{ date: '22.03', label: 'Hamburg' },
		{ date: '05.04', label: 'Munich' },
		{ date: '12.04', label: 'Cologne' },
		{ date: '19.04', label: 'Frankfurt' }
	];

	const releases = [
		{ date: '01.03', label: 'New Album' },
		{ date: '15.02', label: 'Single Release' },
		{ date: '01.02', label: 'EP Drop' },
		{ date: '15.01', label: 'Remix Pack' },
		{ date: '01.01', label: 'Live Session' }
	];
</script>

<div class="fixed top-8 left-8">
	<List title="Shows" items={shows} />
</div>

<div class="fixed top-8 right-8">
	<List title="Releases" items={releases} />
</div>

<div class="fixed bottom-8 left-8">
	<TextInput title="Email" />
</div>

<div class="fixed bottom-8 right-8">
	<TextInput title="Code" />
</div>

<div class="h-screen flex items-center justify-center">
	<img src={bigFishTrouble} alt="BIG TROUBLE" class="w-56 xs:w-56 sm:w-56 md:w-72 h-auto" />
</div>

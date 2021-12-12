<script>
	import Greeting from '$lib/Greeting.svelte';
	import Entry from '$lib/Entry.svelte';
	import EntryModal from '$lib/EntryModal.svelte';
	import supabase from '$lib/db';
	import { goto } from '$app/navigation';
	// Sign out
	async function signOut() {
		const { error } = await supabase.auth.signOut();

		if (error) alert(error.message); // alert if error

		goto('/login');
	}

	// Select entries
	async function getEntries() {
		const { data, error } = await supabase.from('moodEntries').select();
		if (error) alert(error.message);

		return data;
	}
</script>

<Greeting />

<!-- Entries -->
<section class="container px-4 py-3">
	<div class="d-flex justify-content-between">
		<div class="p-2">Mood Log</div>
		<input
			class="btn btn-light mb-2"
			data-bs-toggle="modal"
			data-bs-target="#newEntry"
			type="button"
			value="+ New Entry"
		/>
	</div>

	<div class="list-group mb-3">
		<!-- Individual Entries -->
		{#await getEntries()}
			<p>Fetching data...</p>
		{:then data}
			{#each data as entry}
				<Entry
					date={entry.day + '-' + entry.month + '-' + entry.year}
					mood={entry.mood}
					comment={entry.comment}
				/>
			{/each}
		{:catch error}
			<p>Something went wrong while fetching the data:</p>
			<pre>{error}</pre>
		{/await}
	</div>

	<!-- Sign Out -->
	<section class="container px-4 py-3 text-center">
		<button on:click={signOut} class="btn btn-secondary">Logout</button>
	</section>
</section>

<EntryModal />

<style>
	.btn {
		background-color: #99feff;
		color: black;
	}
</style>

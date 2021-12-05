<script>
	import Greeting from '$lib/Greeting.svelte';
	import Entry from '$lib/Entry.svelte';
	import EntryModal from '$lib/EntryModal.svelte';
	import supabase from '$lib/db';
	async function signOut() {
		const { error } = await supabase.auth.signOut();

		if (error) alert(error.message); // alert if error
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
		<Entry />
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

<script>
	import supabase from '$lib/db';
	let email;

	async function loginUser() {
		const { error } = await supabase.auth.signIn({
			email
		});

		if (error) alert(error.message); // alert if error
	}
</script>

<div class="card mt-5 m-auto text-center" style="width: 24em;">
	<div class="card-body">
		<h5 class="card-title">Welcome</h5>
		<p class="card-text text-muted">Please log-in to continue...</p>
		<form on:submit|preventDefault={loginUser} class="form-floating">
			<input bind:value={email} class="form-control" type="email" />
			<label for="floatingInput">Email address</label>
			<button type="submit" class="btn btn-dark mt-3">Magic</button>
		</form>
	</div>
</div>

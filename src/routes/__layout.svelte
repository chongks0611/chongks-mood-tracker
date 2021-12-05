<script>
	import Navbar from '$lib/Navbar.svelte';
	import { page, session } from '$app/stores';
    import { browser } from '$app/env';
    import { goto } from '$app/navigation';

    // code that runs only in the browser
    if (browser) {
   	 $session = supabase.auth.session(); // set session
   	 redirect();

   	 supabase.auth.onAuthStateChange((userSession) => {
   		 $session = userSession; // set session
   		 redirect();
   	 });
    }

    function redirect() {
   	 //login redirect
   	 if ($session && $page.path === '/') {
   		 goto('/login');
   	 }

   	 //logout redirect
   	 if (!$session && $page.path === '/login') {
   		 goto('/');
   	 }
    }

</script>

<Navbar />
<slot />

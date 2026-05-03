<script>
	import { goto } from '$app/navigation';
	import { fade } from 'svelte/transition';

	async function logout() {
		const identity = (await import('@netlify/identity'))
		await identity.logout();
		goto('/admin/login');
	}
</script>

<div
  in:fade
  class="flex min-h-screen w-full flex-col items-center justify-center font-mono tracking-wider text-gray-700 lowercase"
>
  <p class="tracking-widest mb-8">dashboard</p>
  <button
    onclick={logout}
    class="border border-gray-300 px-6 py-2 text-sm tracking-widest transition hover:border-gray-600 hover:text-black"
  >
    logout
  </button>
</div>

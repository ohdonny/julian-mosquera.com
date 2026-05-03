<script lang="ts">
	import '../app.css';
	import '@fontsource/alegreya-sans';
	import Header from '$lib/Header.svelte';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	let { children } = $props();

	onMount(async () => {
	  const identity = await import('@netlify/identity');
	  const result = await identity.handleAuthCallback();

	  if (result?.type === 'invite' && result.token) {
			const password = prompt('set admin password')
			if (password){
			  await identity.acceptInvite(result.token, password)
			  goto('/admin')
			}
		}
	});
</script>

<div class="flex min-h-screen">
	<Header />

	{@render children()}
</div>

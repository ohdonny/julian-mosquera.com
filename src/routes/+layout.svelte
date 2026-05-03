<script lang="ts">
	import '../app.css';
	import '@fontsource/alegreya-sans';
	import Header from '$lib/Header.svelte';
	import { onMount } from 'svelte';

	let { children } = $props();

	onMount(async () => {
	  const identity = await import('@netlify/identity')
	  await identity.handleAuthCallback()
	})
</script>

<div class="flex min-h-screen">
	<Header />

	{@render children()}
</div>

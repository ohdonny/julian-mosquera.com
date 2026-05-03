<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	onMount(async () => {
		const identity = await import('@netlify/identity')
		const user = await identity.getUser()
		if (!user) goto('/admin/login')
	});
</script>

<slot />

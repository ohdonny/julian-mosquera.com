<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { fade } from 'svelte/transition';
	let email = ""
	let password = ""
	let error = ""

	onMount(async () => {
		const identity = await import('@netlify/identity');
		const user = await identity.getUser()
		if (user != null) goto('/admin')
	});

	async function login() {
	  try{
			const identity = await import('@netlify/identity')
			await identity.login(email, password)
			goto('/admin')
		} catch (e) {
		  error = "Invalid Login. Is this actually Julian?"
		}
	}

</script>

<div
  in:fade
  class="flex min-h-screen w-full flex-col items-center justify-center font-mono tracking-wider text-gray-700 lowercase"
>
  <div class="flex flex-col gap-4 w-64">
    <p class="text-center tracking-widest">admin login</p>
    <input
      type="email"
      bind:value={email}
      placeholder="email"
      class="border-b border-gray-300 bg-transparent py-2 text-sm outline-none placeholder:text-gray-400 focus:border-black"
    />
    <input
      type="password"
      bind:value={password}
      placeholder="password"
      class="border-b border-gray-300 bg-transparent py-2 text-sm outline-none placeholder:text-gray-400 focus:border-black"
    />

    <button
      onclick={login}
      class="mt-2 border border-gray-300 py-2 text-sm tracking-widest transition hover:border-gray-600 hover:text-black"
    >
      enter
    </button>
    <div
        in:fade
        class="border-gray-300 bg-white px-6 py-3 text-xs tracking-widest text-gray-600"
      >
        {error}
      </div>
  </div>
</div>

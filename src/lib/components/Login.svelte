<!-- A Svelte login component leveraging DaisyUI logging in to supabase -->
<script lang="ts">
	import { supabase } from '$lib/supabase';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let email = '';
	let password = '';

	const login = async () => {
		const { data, error } = await supabase.auth.signInWithPassword({
			email,
			password
		});

		if (error) {
			console.error(error);
		} else {
			dispatch('login', { user: data?.user });
		}
	};
</script>

<div class="flex justify-center items-center h-screen">
	<div class="card bg-neutral text-neutral-content w-96">
		<div class="flex flex-col gap-6 self-center w-login card-body">
			<h1 class="text-xl text-center card-title self-center">Login</h1>
			<p class="justify-between flex flex-row">
				<label for="email">Email</label>
				<input type="text" id="email" bind:value={email} />
			</p>
			<p class="justify-between flex flex-row">
				<label for="password">Password</label>
				<input type="password" id="password" bind:value={password} />
			</p>
			<button class="btn btn-primary" on:click={login}>Login</button>
		</div>
	</div>
</div>

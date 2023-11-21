<script lang="ts">
	import '../style.css';

	import CreateTodo from '$lib/components/CreateTodo.svelte';
	import { supabase } from '$lib/supabase';
	import { Authenticated, SupabaseApp, Unauthenticated } from 'supasveltekit';
	import Login from '$lib/components/Login.svelte';

	const createTodoHandler = async (todo: any) => {
		const { data, error } = await supabase.from('todos').insert(todo);
		if (error) {
			console.error(error);
		}
	};

	const logout = async () => {
		const { error } = await supabase.auth.signOut();

		if (error) {
			console.error(error);
		}
	};
</script>

<SupabaseApp {supabase}>
	<Unauthenticated>
		<Login />
	</Unauthenticated>

	<Authenticated>
		<div class="h-screen flex flex-col">
			<div class="navbar bg-primary text-primary-content">
				<div class="navbar-start">
					<a class="btn btn-ghost normal-case text-xl" href="/">Awesome Todo App</a>
				</div>

				<div class="navbar-end">
					<CreateTodo
						on:create={async (createEvent) => await createTodoHandler(createEvent.detail)}
					/>
					<button class="btn btn-secondary ml-4" on:click={logout}>Logout</button>
				</div>
			</div>

			<div class="flex flex-1 m-6">
				<slot />
			</div>

			<div class="p-8 text-center bg-base-200 text-base-content">
				<p>
					Powered by <a
						href="https://github.com/OpenFrenchFries/supasveltekit"
						target="_blank"
						class="hover:underline">SupaSvelteKit</a
					> 🚀
				</p>
			</div>
		</div>
	</Authenticated>
</SupabaseApp>

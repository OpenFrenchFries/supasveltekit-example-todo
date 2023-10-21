<script lang="ts">
	import Card from '$lib/components/Card.svelte';
	import type { Todo } from '$lib/types/todo';
	import { supabase } from '../lib/supabase';
	import { SupabaseApp, Collection } from 'supasveltekit';

	const table = 'todos';

	// Function to update a todo in supabase
	const updateTodo = async (todo: Todo) => {
		const { data, error } = await supabase.from(table).update(todo).eq('id', todo.id).single();

		if (error) {
			console.error(error);
		}
		return data;
	};

	// Function to delete a todo in supabase
	const deleteTodo = async (todo: Todo) => {
		const { error } = await supabase.from(table).delete().eq('id', todo.id).single();

		if (error) {
			console.error(error);
		}
	};
</script>

<SupabaseApp {supabase}>
	<div class="flex flex-col gap-6">
		<Collection {table} let:payload let:error realtime={true}>
			{#if !payload}
				<p>Loading...</p>
			{:else if error}
				<p>{error.message}</p>
			{:else}
				{#each payload.sort() as entry}
					<Card
						entity={entry}
						on:done={async (updateEvent) => await updateTodo(updateEvent.detail)}
                        on:delete={async (deleteEvent) => await deleteTodo(deleteEvent.detail)}
					/>
				{/each}
			{/if}
			<div slot="loading">
				<p>Loading...</p>
			</div>
		</Collection>
	</div>
</SupabaseApp>

<!-- A Svelte component to create a popup using DaisyUI to create a todo --->
<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let title = '';
	let desc = '';

	const showModal = () => {
		const modal: any = document.getElementById('create-todo-modal');
		modal?.showModal();
	};

	const createTodo = async () => {
		dispatch('create', { title, desc });
        const modal: any = document.getElementById('create-todo-modal');
        modal?.close();
	};
</script>

<button class="btn" on:click={() => showModal()}>Add ToDo</button>
<dialog id="create-todo-modal" class="modal modal-bottom sm:modal-middle">
	<div class="modal-box">
		<h3 class="font-bold text-lg">New todo</h3>
		<div class="form-control">
			<label class="label">
				<span class="label-text">Title</span>
				<input class="input" type="text" bind:value={title} />
			</label>
		</div>
		<div class="form-control">
			<label class="label">
				<span class="label-text">Description</span>
				<input class="input" type="text" bind:value={desc} />
			</label>
		</div>
		<div class="modal-action">
			<button class="btn btn-primary btn-outline" on:click={createTodo}>Create</button>
			<form method="dialog">
				<button class="btn btn-secondary btn-outline">Cancel</button>
			</form>
		</div>
	</div>
</dialog>

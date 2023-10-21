<script lang="ts">
	import type { Todo } from '$lib/types/todo';
	import { createEventDispatcher } from 'svelte';
	import TrashButton from './TrashButton.svelte';
	export let entity: Todo | null = null;

	//dispatcher to notify when entity is updated
	const dispatch = createEventDispatcher();
</script>

{#if !!entity}
	<div class="card w-96 shadow-xl bg-neutral text-neutral-content indicator">
		{#if entity.done}
			<span class="indicator-item badge badge-success">done</span>
		{/if}
		<div class="card-body">
			<h2 class="card-title">
				{entity.title}
			</h2>
			<p>{entity.desc}</p>
			<div class="card-actions justify-between flex flex-row pt-3">
				<input
					type="checkbox"
					class="toggle toggle-success self-center"
					checked={entity.done}
					on:change={() => dispatch('done', { ...entity, done: !entity?.done })}
				/>
				<TrashButton on:click={() => dispatch("delete", entity)} />
			</div>
		</div>
	</div>
{/if}

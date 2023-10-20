<script lang="ts">
    import type { Todo } from "$lib/types/todo";
	export let entity: Todo | undefined = null;
</script>

{#if !!entity}
	<div class="card w-96 bg-base-100 shadow-xl">
		<div class="card-body">
			<h2 class="card-title">{entity.title}</h2>
			<p>{entity.desc}</p>
			<div class="card-actions justify-end">
				<button class="btn btn-primary">Done</button>
			</div>
		</div>
	</div>
{/if}

<script lang="ts">
	import '../style.css';

    import CreateTodo from '$lib/components/CreateTodo.svelte';
    import { supabase } from '$lib/supabase';

    const createTodoHandler = async (todo: any) => {
        const { data, error } = await supabase.from('todos').insert(todo);
        if (error) {
            console.error(error);
        }
    };
</script>

<div class="navbar bg-primary text-primary-content">
	<div class="navbar-start">
		<a class="btn btn-ghost normal-case text-xl" href="/">Awesome Todo App</a>
	</div>
	
	<div class="navbar-end">
        <CreateTodo on:create={async (createEvent) => await createTodoHandler(createEvent.detail)} />
    </div>
</div>
<div class="m-6">
	<slot />
</div>

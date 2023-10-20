<script lang="ts">
    import Card from "$lib/components/Card.svelte";
    import { supabase } from "../lib/supabase";
    import { SupabaseApp, Collection } from "supasveltekit";

    const table = "todos";
</script>

<SupabaseApp {supabase}>
    <h1 class="text-5xl font-bold">Demo todo app</h1>

    <h2 class="text-4xl font-bold">Todo list</h2>

    <Collection table={table} let:payload let:error realtime={true}>
        {#if !payload}
            <p>Loading...</p>
        {:else if error}
            <p>{error.message}</p>
        {:else}
            {#each payload as entry}
                <Card entity={entry}></Card>
            {/each}
        {/if}
        <div slot="loading">
            <p>Loading...</p>
        </div>
    </Collection>
</SupabaseApp>



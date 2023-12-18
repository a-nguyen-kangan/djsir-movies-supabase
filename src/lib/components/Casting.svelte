<script>
    import { createEventDispatcher } from 'svelte';

    export let casting = [];
    const dispatch = createEventDispatcher();

    function selectActor(actor) {
        console.log('Selecting actor:', actor);
        dispatch('actorSelect', { actor });
    }
</script>

<div class="casting-list">
    {#each casting as cast}
        <span class="actor-name" on:click={() => selectActor(cast.Actor)}>
            {cast.Actor.Name}
        </span>
    {/each}
</div>

<style>
    .actor-name {
        cursor: pointer;
        color: blue; 
    }
    .actor-name:hover {
        text-decoration: underline;
    }
</style>

<script lang="ts">
    import { Button, Heading, Input } from 'flowbite-svelte';
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    let searchTitle = '';


    const search = () => {
        dispatch('titleSearch', {
            titleSearch: searchTitle
        });
    }
</script>

<Heading>Movie Title Search</Heading>
<div>
    <Input class="m-5" type="text" id="movie_title" placeholder="" required bind:value={searchTitle} />
    <Button class="mb-5 ml-5" on:click={search}>Search</Button>
</div>
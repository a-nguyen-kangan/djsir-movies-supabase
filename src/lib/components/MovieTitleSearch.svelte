<script lang="ts">
    import { Button, Heading, Input } from 'flowbite-svelte';
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
    let searchTitle = '';

    const search = () => {
        dispatch('titleSearch', { titleSearch: searchTitle });
    };

    const handleSubmit = (event) => {
        event.preventDefault();
        search();
    };
</script>

<Heading>Movie Title Search</Heading>
<form on:submit={handleSubmit}>
    <div class="m-5">
        <Input type="text" id="movie_title" aria-label="Search Movie Title"
               placeholder="Enter movie title..." required bind:value={searchTitle} />
        <Button class="mb-5 ml-5" type="submit">Search</Button>
    </div>
</form>

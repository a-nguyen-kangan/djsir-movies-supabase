<script>
    import { Heading } from 'flowbite-svelte';
    import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';
    import Casting from '$lib/components/Casting.svelte';
    import { createEventDispatcher } from 'svelte';

    export let movies = [];
    
    const dispatch = createEventDispatcher();

    function handleActorSelect(actor) {
        console.log('Received in MovieResults:', event.detail);
        dispatch('actorSelect', actor);
    }

</script>

<hr>
<Heading class="my-5">Movie Results</Heading>
<Table striped={true}>
    <TableHead>
        <TableHeadCell>MovieNo</TableHeadCell>
        <TableHeadCell>Title</TableHeadCell>
        <TableHeadCell>Runtime</TableHeadCell>
        <TableHeadCell>Director Name</TableHeadCell>
        <TableHeadCell>Casting</TableHeadCell>
    </TableHead>
    <TableBody>
        {#each movies as movie}
        <TableBodyRow>
            <TableBodyCell>{movie.MovieNo}</TableBodyCell>
            <TableBodyCell>{movie.Title}</TableBodyCell>
            <TableBodyCell>{movie.Runtime}</TableBodyCell>
            <TableBodyCell>{movie.Director.Name}</TableBodyCell>
            <TableBodyCell>
                <Casting casting={movie.Casting} on:actorSelect={handleActorSelect} />
            </TableBodyCell>
        </TableBodyRow>
        {/each}
    </TableBody>
</Table>

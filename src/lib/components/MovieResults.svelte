<script>
    import { Heading } from 'flowbite-svelte'
    import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';

    export let movies = [];
</script>
<hr>
<Heading class="my-5">Movie Results</Heading>
<Table striped={true}>
<TableHead>
    <TableHeadCell>MovieNo</TableHeadCell>
    <TableHeadCell>Title</TableHeadCell>
    <TableHeadCell>RunTime</TableHeadCell>
    <TableHeadCell>Director Name</TableHeadCell>
</TableHead>
<TableBody>
    {#each movies as movie}
    <TableBodyRow>
        <TableBodyCell>{movie.MovieNo}</TableBodyCell>
        <TableBodyCell>{movie.Title}</TableBodyCell>
        <TableBodyCell>{movie.RunTime}</TableBodyCell>
        <TableBodyCell>{movie.Directors.Name}</TableBodyCell>
    </TableBodyRow>
    {/each}
</TableBody>
</Table>
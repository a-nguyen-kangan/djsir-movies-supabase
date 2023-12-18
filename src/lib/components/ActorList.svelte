<script>
    import { Heading } from 'flowbite-svelte';
    import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';

    export let actors = [];

</script>

<hr>
<Heading class="my-5">Actor Results</Heading>
<Table striped={true}>
    <TableHead>
        <TableHeadCell>Actor ID</TableHeadCell>
        <TableHeadCell>Name</TableHeadCell>
        <TableHeadCell>Year of Birth</TableHeadCell>
    </TableHead>
    <TableBody>
        {#each actors as actor}
        <TableBodyRow>
            <TableBodyCell>{actor.ActorId}</TableBodyCell>
            <TableBodyCell>{actor.Name}</TableBodyCell>
            <TableBodyCell>{actor['Year Of Birth']}</TableBodyCell>
        </TableBodyRow>
        {/each}
    </TableBody>
</Table>


<style>
    .selected-actor-details {
        margin-top: 20px;
    }
</style>

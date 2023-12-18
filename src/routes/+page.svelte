<script>
    import MovieResults from "$lib/components/MovieResults.svelte";
    import MovieTitleSearch from "$lib/components/MovieTitleSearch.svelte";
    import ActorList from '$lib/components/ActorList.svelte';
    import { createClient } from "@supabase/supabase-js";
    import { onMount } from "svelte";

    const supabaseUrl = 'https://tclixqgzprlwmxipzwwx.supabase.co';
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InRjbGl4cWd6cHJsd214aXB6d3d4Iiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTcwMTY0OTEwNywiZXhwIjoyMDE3MjI1MTA3fQ.eHQMsKVuPtC3Sieg6MFawkTIkPCR25Me2oldEk3jzqk';

    const supabaseClient = createClient(supabaseUrl, supabaseKey);

    
    let moviesList = [];
    let selectedActor = null;

    
    onMount(() => {
    });

    const getMoviesByTitle = async (event) => {
        let searchString = '%'+ event.detail.titleSearch + '%';

        const { data, error } = await supabaseClient
            .from('Movies')
            .select(`
                MovieNo,
                Title,
                Runtime,
                Director ( Name ),
                Casting ( ActorId, Actor( Name, "Year of Birth" ))
            `)
            .ilike('Title', searchString)

        if (error) {
            alert(error.message);
            return;
        }

        moviesList = data;
    }
    
    function handleActorSelected(event) {
        console.log('Received in +page:', event.detail);
        selectedActor = event.detail.actor;
    }



</script>

<MovieTitleSearch on:titleSearch={getMoviesByTitle} />
<MovieResults movies={moviesList} on:actorSelect={handleActorSelected} />
<ActorList actors={selectedActor ? [selectedActor] : []} />


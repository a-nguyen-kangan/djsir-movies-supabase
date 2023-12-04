<script>
    import MovieResults from "$lib/components/MovieResults.svelte";
    import MovieTitleSearch from "$lib/components/MovieTitleSearch.svelte";
    import { createClient } from "@supabase/supabase-js";
    import { onMount } from "svelte";

    const supabaseUrl = 'https://xmutyxjqddxwqqacfxwt.supabase.co';
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InhtdXR5eGpxZGR4d3FxYWNmeHd0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDEwNDI3MDUsImV4cCI6MjAxNjYxODcwNX0.p2Rk9nFxWAtwVPSOL7VKnq6T0JnJzcoazPBJU3frRvU';

    const supabaseClient = createClient(supabaseUrl, supabaseKey);

    let moviesList = [];

    onMount(() => {
        getMovies();
    });

    // the below is equivalent to:  async function getMovies() {...}
    const getMovies = async () => {
        const { data, error } = await supabaseClient
            .from('Movies')
            .select(`
                    *,
                    Directors (
                    *
                    )
                `
            );

        if (error) {
            alert(error.message);
            return;
        }

        moviesList = data;
        console.log(moviesList);
    }

    const getMoviesByTitle = async (event) => {
        let searchString = '%'+ event.detail.titleSearch + '%';

        const { data, error } = await supabaseClient
            .from('Movies')
            .select(`
                    *,
                    Directors (
                    *
                    )
                `)
            .ilike('Title', searchString)

        if (error) {
            alert(error.message);
            return;
        }

        moviesList = data;
    }
</script>

<MovieTitleSearch on:titleSearch={getMoviesByTitle}/>
<MovieResults movies={moviesList} />

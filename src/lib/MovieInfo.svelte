<script lang="ts">
    import { onMount } from "svelte";

    export let activeMovie = "12 Years a Slave";
    let movie_data;
    let year;
    let overview;
    onMount(() => {
        updateMovieData(activeMovie);
    });
    const url = import.meta.env.VITE_MOVIEDATA_URL;

    $: updateMovieData(activeMovie);

    async function updateMovieData(movie) {
        let movieurl = url + `${movie}.json`;
        console.log(movieurl);
        let resp = await fetch(movieurl);
        movie_data = await resp.json();
        year = movie_data["release_date"].split("-")[0];
        console.log(movie_data);
    }
</script>

{#if movie_data}
    <h2 class="text-xl text-center">
        <a
            class="text-slate-300 underline"
            href="https://www.themoviedb.org/movie/{movie_data.id}"
            >{movie_data.title}</a
        >
        ({year})
    </h2>

    <p class="text-justify mt-1">
        {movie_data.overview}
    </p>
    <div class="mt-4 text-right">
        More on: <a
            class="mt-4 p-1 font-semibold text-sm bg-slate-500 text-white rounded-none shadow-sm"
            href="https://www.themoviedb.org/movie/{movie_data.id}
        "
        >
            TMDB
        </a>
        <a
            class="mt-4 p-1 font-semibold text-sm bg-slate-500 text-white rounded-none shadow-sm"
            href="https://www.letterboxd.com/film/{activeMovie}
        "
        >
            Letterboxd</a
        >
    </div>
{/if}

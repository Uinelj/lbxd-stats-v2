<script lang="ts">
    import { onMount } from "svelte";

    let movies = [];
    export let activeMovie;

    onMount(async () => {
        const wl_url = "https://uinelj.github.io/lbxd-stats/res/watchlist.json";
        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const res = await fetch(wl_url, options);
        movies = await res.json();
        movies.sort();
    });
</script>

<div>
    <select
        name="movies"
        id="movies"
        bind:value={activeMovie}
        class="text-slate-800 block mx-auto mb-8 p-2"
    >
        <option value="">Pick a movie</option>
        {#each movies as movie}
            <option value={movie}>{movie.split("-").join(" ")}</option>
        {/each}
    </select>
</div>

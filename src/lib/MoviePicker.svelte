<script lang="ts">
    import { onMount } from "svelte";

    let movies: Object = [];
    export let activeMovie: String;

    const sortObject = (o) =>
        Object.keys(o)
            .sort()
            .reduce((r, k) => ((r[k] = o[k]), r), {});
    onMount(async () => {
        const wl_url = import.meta.env.VITE_WATCHLIST_URL;

        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const res = await fetch(wl_url, options);
        const movies_unsorted = await res.json();

        movies = sortObject(movies_unsorted);
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
        {#each Object.entries(movies) as [id, title]}
            <option value={id}>{title}</option>
        {/each}
    </select>
</div>

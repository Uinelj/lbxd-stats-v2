<script lang="ts">
    import { onMount } from "svelte";
    //import { Index } from "lunr";
    import lunr from "lunr";
    // import lunr from "lunr";

    let movies = [];
    let movies_for_index = [];
    let idx;
    export let activeMovie;

    onMount(async () => {
        const wl_url = "http://localhost:5173/res/watchlist.json";
        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const res = await fetch(wl_url, options);
        movies = await res.json();
        movies.sort();

        movies.forEach(function (movieid) {
            movieid = movieid.split("-").join(" ");
            movies_for_index.push({ name: movieid, text: movieid });
        });

        console.log(movies_for_index);
        idx = lunr(function () {
            this.ref("name");
            this.field("text");

            movies_for_index.forEach(function (doc) {
                // doc = doc.split("-").join(" ");
                this.add(doc);
            }, this);
        });
    });

    //build index

    // console.log(idx);
    console.log(idx.search("avatar"));

    // var documents = [
    //     {
    //         name: "Lunr",
    //         text: "Lunr",
    //     },
    //     {
    //         name: "React",
    //         text: "React",
    //     },
    //     {
    //         name: "Lodash",
    //         text: "Lodash",
    //     },
    // ];

    // var idx = lunr(function () {
    //     this.ref("name");
    //     this.field("text");

    //     documents.forEach(function (doc) {
    //         this.add(doc);
    //     }, this);
    // });

    console.log(idx);
</script>

<div>
    <label for="movielist">Pick a movie:</label>
    <select
        name="movies"
        id="movies"
        bind:value={activeMovie}
        class="text-slate-800"
    >
        {#each movies as movie}
            <option value={movie}>{movie}</option>
        {/each}
    </select>
</div>
<!-- <svelte:head>
    <script type="module">
        import "https://unpkg.com/lunr/lunr.js";
    </script>
</svelte:head> -->

<script lang="ts">
    import { onMount } from "svelte";

    export let activeMovie = "12-years-a-slave";
    let movie_data;
    let overview;
    onMount(() => {
        updateMovieData(activeMovie);
    });
    const url = import.meta.env.VITE_MOVIEDATA_URL;

    $: updateMovieData(activeMovie);

    async function updateMovieData(movie) {
        let movieurl = url + `${movie}.json`;
        console.log(movieurl);
        let movie_data = await fetch(movieurl);
        movie_data = await movie_data.json();
        overview = movie_data["overview"];
        console.log(movie_data);
    }
</script>

<h2>{movie_data.title}</h2>
<p>
    {overview}
</p>
<table>
    <thead>
        <tr>
            <th colspan="2">The table header</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>The table body</td>
            <td>with two columns</td>
        </tr>
    </tbody>
</table>

<script lang="ts">
    import { onMount } from "svelte";
    export let movie: String = "robots";
    let graph;
    //$: graph = renderGraph(movie);
    $: renderGraph(movie);

    async function renderGraph(movieid: String) {
        const url = `http://localhost:5173/res/graph_data/${movie}.json`;
        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const resp = await fetch(url, options);
        const data = await resp.json();

        Plotly.newPlot(graph, data);
    }

    onMount(async () => {
        renderGraph(movie);
    });
</script>

<h2>{movie} graph</h2>
<div bind:this={graph} />
<svelte:head>
    <script type="module">
        import "https://cdn.plot.ly/plotly-2.18.2.min.js";
    </script>
</svelte:head>

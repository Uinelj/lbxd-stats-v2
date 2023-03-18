<script lang="ts">
    import { onMount } from "svelte";
    export let movie: String = "robots";

    const divId = "gd";
    onMount(async () => {
        const url = `http://localhost:5173/res/graph_data/${movie}.json`;
        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const resp = await fetch(url, options);
        const data = await resp.json();

        Plotly.newPlot(divId, data);
    });
</script>

<h2>{movie} graph</h2>
<div id={divId} />
<svelte:head>
    <script type="module">
        import "https://cdn.plot.ly/plotly-2.18.2.min.js";
    </script>
</svelte:head>

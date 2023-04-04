<script lang="ts">
    import { onMount } from "svelte";
    export let movie: String = "robots";
    export let useAbsoluteRatingRange: boolean = false;
    let graph;

    $: renderGraph(movie, useAbsoluteRatingRange);

    async function renderGraph(
        movieid: String,
        useAbsoluteRatingRange: boolean
    ) {
        if (movieid == undefined) {
            return;
        }
        const url = import.meta.env.VITE_GRAPHDATA_URL + movie + ".json";
        const options = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        };
        const resp = await fetch(url, options);
        const data = await resp.json();

        const layout = {
            title: movieid,
            paper_bgcolor: "rgba(0, 0, 0, 0)",
            plot_bgcolor: "rgba(0, 0, 0, 0)",
            font: { color: "rgb(226 232 240)" },
            yaxis: {
                gridcolor: "rgb(71 85 105)",
                // range: [0.5, 5],
                range: useAbsoluteRatingRange ? [0.5, 5] : null,
            },
            xaxis: { gridcolor: "rgb(71 85 105)" },
            display_mode_bar: false,
            colorway: ["#000000"],
            showlegend: true,
        };

        data["layout"] = layout;

        // remove notes on each data point
        data["data"][0]["text"] = [];
        Plotly.newPlot(graph, data, { display_mode_bar: false });
    }

    onMount(async () => {
        renderGraph(movie, useAbsoluteRatingRange);
    });
</script>

<div bind:this={graph} />
<svelte:head>
    <script type="module">
        import "https://cdn.plot.ly/plotly-2.18.2.min.js";
    </script>
</svelte:head>

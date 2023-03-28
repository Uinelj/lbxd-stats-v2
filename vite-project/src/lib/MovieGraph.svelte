<script lang="ts">
    import { onMount } from "svelte";
    export let movie: String = "robots";
    let graph;

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

        // let layout = { legend: { bgcolor: "000000" } };
        const layout = {
            title: movieid,
            // legend: {
            //     // paper_bgcolor: "rgba(0, 0, 0, 0)",
            //     // plot_bgcolor: "rgba(0, 0, 0, 0)",
            //     paper_bgcolor: "#000000",
            //     plot_bgcolor: "#000000",
            // },
            paper_bgcolor: "rgba(0, 0, 0, 0)",
            plot_bgcolor: "rgba(0, 0, 0, 0)",
            displayModeBar: false,
            showlegend: true,
        };

        data["layout"] = layout;

        Plotly.newPlot(graph, data, { displayModeBar: false });
    }

    onMount(async () => {
        renderGraph(movie);
    });
</script>

<div bind:this={graph} />
<svelte:head>
    <script type="module">
        import "https://cdn.plot.ly/plotly-2.18.2.min.js";
    </script>
</svelte:head>

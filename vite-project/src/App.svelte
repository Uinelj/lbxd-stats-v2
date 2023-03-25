<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import MoviePicker from "./lib/MoviePicker.svelte";
  import MovieGraph from "./lib/MovieGraph.svelte";

  let activeMovie;
</script>

<main class="my-0 mx-auto max-w-7xl ">
  <h1 class="text-2xl m-auto text-right">Letterstonks</h1>
  <div class="mx-auto my-40">
    <p>Track the rating evolution of movies.</p>
    <p>
      Note that movies ratings are monitored and logged periodically, so you
      can't go back in time.
    </p>
  </div>

  <MoviePicker bind:activeMovie />
  <MovieGraph bind:movie={activeMovie} />
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>

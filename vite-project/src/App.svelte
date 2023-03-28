<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import MoviePicker from "./lib/MoviePicker.svelte";
  import MovieGraph from "./lib/MovieGraph.svelte";

  let activeMovie;
</script>

<main class="my-0 mx-auto max-w-7xl ">
  <h1 class="text-2xl m-auto text-right mt-8 mr-2">Letterstonks</h1>
  <div class="mx-auto my-20">
    <p>Track the rating evolution of movies!</p>
    <p>
      Note that movies ratings are monitored and logged periodically, so you
      can't go back in time.
    </p>
  </div>

  <MoviePicker bind:activeMovie />
  <MovieGraph bind:movie={activeMovie} />

  <div class="p-2">
    <h2 class="text-xl">How does that work?</h2>
    <p class="m-2 p-2 max-w-md">
      Each 12 hours, I get the most popular movies of the week/year/all time,
      and add them in a watchlist if they aren't yet there. Then, for the new
      additions, I get their current rating.
      <br />
      Then, I get the rating of <code>n</code>
      movies that are already in the watchlist. The <code>n</code> is defined so
      that all movies are updated at least once a week via random sampling.
    </p>
  </div>
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

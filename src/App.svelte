<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import MoviePicker from "./lib/MoviePicker.svelte";
  import MovieGraph from "./lib/MovieGraph.svelte";
  import MovieInfo from "./lib/MovieInfo.svelte";

  const tmdb_baseurl = "https://image.tmdb.org/t/p/w1280";
  const moviedata_baseurl = import.meta.env.VITE_MOVIEDATA_URL;

  async function getBackdrop(movie: string) {
    const data_url = moviedata_baseurl + `${movie}.json`;
    const resp = await fetch(data_url);
    const data = await resp.json();
    const backdrop_path = tmdb_baseurl + data["backdrop_path"];
    return `url(${backdrop_path})`;
    console.log(data);
  }

  let activeMovie;
  let useAbsoluteRatingRange;
  let ratingRange = "relative";
  let backdrop_css = null;

  function changeRange() {
    useAbsoluteRatingRange = !useAbsoluteRatingRange;
    if (useAbsoluteRatingRange) {
      ratingRange = "absolute";
    } else {
      ratingRange = "relative";
    }
  }
  $: getBackdrop(activeMovie).then((url) => (backdrop_css = url));
</script>

<main
  class="backdrop bg-cover bg-no-repeat bg-fixed m-0 p-0 h-screen text-slate-200"
  style="--backdrop_css: {backdrop_css};"
>
  <div class="my-0 mx-auto max-w-7xl backdrop-blur-lg">
    <h1 class="text-2xl m-auto text-right pt-8 mr-2 font-serif">
      Letterstonks
    </h1>
    <div class="mx-auto my-20 p-20">
      <p>Track the rating evolution of movies!</p>
      <p>
        Note that movies ratings are monitored and logged periodically, so you
        can't go back in time.
      </p>
    </div>

    <MoviePicker bind:activeMovie />
    <MovieGraph bind:movie={activeMovie} bind:useAbsoluteRatingRange />
    <button
      class="mx-4 px-4 py-2 font-semibold text-sm bg-slate-500 text-white rounded-none shadow-sm ml-4"
      on:click={changeRange}
      type="button"
    >
      Rating range: {ratingRange}
    </button>

    <div class="flex flex-row md:flex-1">
      <div class="p-2 basis-1/2 md:basis-full">
        <MovieInfo bind:activeMovie />
      </div>

      <div class="p-2 basis-1/2 md:basis-full">
        <h2 class="text-xl">How does that work?</h2>
        <p class="m-2 p-2 max-w-md">
          Each 12 hours, I get the most popular movies of the week/year/all
          time, and add them in a watchlist if they aren't yet there. Then, for
          the new additions, I get their current rating.
          <br />
          Then, I get the rating of <code>n</code>
          movies that are already in the watchlist. The <code>n</code> is defined
          so that all movies are updated at least once a week via random sampling.
        </p>
      </div>
    </div>
  </div>
</main>

<style>
  .backdrop {
    background-image: linear-gradient(
        to top,
        rgba(30, 41, 59, 0.8),
        rgba(71, 85, 105, 0.8)
      ),
      var(
        --backdrop_css,
        linear-gradient(to top, rgba(30, 41, 59, 0.8), rgba(71, 85, 105, 0.8))
      );
  }
</style>

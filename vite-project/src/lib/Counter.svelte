<script lang="ts">
  let count: number = 0;
  const increment = () => {
    count += 1;
  };

  const reset = () => {
    count = 0;
  };
</script>

<div class="inline-flex">
  <button
    on:click={increment}
    class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l"
  >
    count is {count}
  </button>
  <button
    on:click={reset}
    class="bg-gray-200 hover:bg-gray-300 text-gray-800 font-bold py-2 px-4 rounded-r"
  >
    reset
  </button>
</div>

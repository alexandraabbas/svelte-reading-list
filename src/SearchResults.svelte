<script>
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";

  export let results;

  const dispatch = createEventDispatcher();

  function handleAdd(data) {
    dispatch("add", data.detail);
  }
</script>

<style>
  .search-results {
    list-style: none;
    display: grid;
    gap: 40px 20px;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    padding: 20px;
  }
</style>

<ul class="search-results">
  {#each results as result (result.id)}
    <Card on:add={handleAdd} item={result} />
  {/each}
</ul>

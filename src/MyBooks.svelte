<script>
  import Book from "./Book.svelte";
  import { createEventDispatcher } from "svelte";

  export let books;

  const dispatch = createEventDispatcher();

  function handleDelete(data) {
    books = books.filter(item => item.id !== data.detail);
    dispatch("delete", books);
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
  h1 {
    text-align: left;
    margin-left: 20px;
  }
  p {
    padding-top: 50px;
    font-size: 18px;
  }
</style>

<h1>📖 My books</h1>
{#if books.length == 0}
  <p>You don't have any books yet. 🤭</p>
{:else}
  <ul class="search-results">
    {#each books as book (book.id)}
      <Book on:delete={handleDelete} {book} />
    {/each}
  </ul>
{/if}

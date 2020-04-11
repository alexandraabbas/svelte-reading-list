<script>
  import Book from "./Book.svelte";

  export let books;

  function handleDelete(data) {
    books = books.filter(item => item.id !== data.detail);
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
</style>

<h1>📖 My books</h1>
<ul class="search-results">
  {#each books as book (book.id)}
    <Book on:delete={handleDelete} {book} />
  {/each}
</ul>

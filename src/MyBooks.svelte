<script>
  import Book from "./Book.svelte";

  export let books;
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

<p>myBooks length: {books.length}</p>
<ul class="search-results">
  {#each books as book (book.id)}
    <Book {book} />
  {/each}
</ul>

<script>
  import Search from "./Search.svelte";
  import SearchResults from "./SearchResults.svelte";
  import MyBooks from "./MyBooks.svelte";

  import { onMount } from "svelte";
  import { db } from "./firebase";

  let searchQuery = "";
  let searchTerm = null;
  let searchResults = [];
  let myBooks = [];

  const API_KEY = "BOOKS_API_KEY";

  async function getResult() {
    const endpoint = `https://www.googleapis.com/books/v1/volumes?q=${searchTerm}&key=${API_KEY}`;

    fetch(endpoint)
      .then(response => response.json())
      .then(data => (searchResults = [...data.items]))
      .catch(error => alert(error));
  }

  function handleSubmit() {
    searchTerm = searchQuery.trim();
    getResult();
  }

  async function getMyBooks() {
    const snapshot = await db.collection("books").get();

    const documents = [];
    snapshot.forEach(doc => {
      documents.push({ id: doc.id, ...doc.data() });
    });

    return documents;
  }

  onMount(() =>
    getMyBooks().then(data => {
      myBooks = data;
    })
  );

  function handleAdd(data) {
    myBooks = [...myBooks, data.detail];
  }

  function handleDelete(data) {
    myBooks = data.detail;
  }
</script>

<style>
  .App {
    width: 100%;
    max-width: 1500px;
    margin: 0 auto 50px;
    text-align: center;
  }
  h1 {
    font-size: 50px;
    margin-top: 30px;
    margin-bottom: 30px;
  }
</style>

<main class="App">
  <h1>📚 Reading list app</h1>
  <Search bind:query={searchQuery} {handleSubmit} />
  <SearchResults on:add={handleAdd} results={searchResults} />
  <MyBooks on:delete={handleDelete} books={myBooks} />
</main>

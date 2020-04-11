<script>
  import { db } from "./firebase";
  import { createEventDispatcher } from "svelte";

  export let item;

  const dispatch = createEventDispatcher();

  let id = item.id;
  let infoLink = item.volumeInfo.infoLink;
  let imageLink = item.volumeInfo.imageLinks.smallThumbnail;
  let title = item.volumeInfo.title;
  let authors = item.volumeInfo.authors;

  function add() {
    let book = {
      title,
      authors,
      infoLink,
      imageLink,
      label: "To Read",
      created: new Date(Date.now())
    };

    db.collection("books")
      .add(book)
      .then(function(docRef) {
        console.log("Document written with ID: ", docRef.id);
        dispatch("add", book);
      })
      .catch(function(error) {
        console.error("Error adding document: ", error);
      });
  }
</script>

<style>
  .card {
    transition: 0.3s;
    border-radius: 5px;
    border: 1px solid #e2e2e2;
  }
  .card:hover {
    box-shadow: 0 4px 8px 0 rgba(100, 100, 100, 0.2);
  }
  .container {
    padding: 2px 16px;
  }
  img {
    height: 189px;
    margin-top: 12px;
    border: 1px solid #b9b9b9;
  }
  a {
    color: #333;
  }
  .add {
    padding-bottom: 8px;
    padding-left: 25px;
    padding-right: 25px;
    border: #f4f4f4;
    cursor: pointer;
    margin-bottom: 15px;
  }
</style>

<li>
  <div class="card">
    <img src={imageLink} alt="Thumbnail" />
    <div class="container">
      <a href={infoLink}>
        <h4>
          <b>{title}</b>
        </h4>
      </a>
      <p>{authors}</p>
    </div>
    <button class="add" on:click={add}>✅ Add to My books</button>
  </div>
</li>

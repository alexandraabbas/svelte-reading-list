<script>
  import { db } from "./firebase";
  export let item;

  let id = item.id;
  let infoLink = item.volumeInfo.infoLink;
  let imageLink = item.volumeInfo.imageLinks.smallThumbnail;
  let title = item.volumeInfo.title;
  let authors = item.volumeInfo.authors;

  function add() {
    db.collection("books")
      .add({
        title,
        authors,
        infoLink,
        imageLink,
        label: "To Read",
        created: new Date(Date.now())
      })
      .then(function(docRef) {
        console.log("Document written with ID: ", docRef.id);
      })
      .catch(function(error) {
        console.error("Error adding document: ", error);
      });
  }
</script>

<style>
  .card {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    transition: 0.3s;
    border-radius: 5px;
  }
  .card:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  }
  .container {
    padding: 2px 16px;
  }
  img {
    border-radius: 5px 5px 0 0;
    height: 189px;
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
    <button on:click={add}>Add to My Books</button>
  </div>
</li>

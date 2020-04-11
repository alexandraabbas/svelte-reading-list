<script>
  import { db } from "./firebase";
  export let book;

  let infoLink = book.infoLink;
  let imageLink = book.imageLink;
  let title = book.title;
  let authors = book.authors;

  function del() {
    db.collection("books")
      .doc(book.id)
      .delete()
      .then(function() {
        console.log("Document successfully deleted!");
      })
      .catch(function(error) {
        console.error("Error removing document: ", error);
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
    <button on:click={del}>Delete from My Books</button>
  </div>
</li>

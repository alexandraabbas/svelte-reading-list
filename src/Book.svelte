<script>
  import { db } from "./firebase";
  export let book;

  let infoLink = book.infoLink;
  let imageLink = book.imageLink;
  let title = book.title;
  let authors = book.authors;
  let label = book.label;

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

  function update(label) {
    db.collection("books")
      .doc(book.id)
      .set(
        {
          label: label
        },
        { merge: true }
      )
      .then(function() {
        console.log("Document successfully updated!");
      })
      .catch(function(error) {
        console.error("Error updating document: ", error);
      });
  }

  function updateLabel() {
    if (label == "To Read") {
      label = "Reading";
      update(label);
    } else if (label == "Reading") {
      label = "Finished";
      update(label);
    } else {
      label = "To Read";
      update(label);
    }
  }
</script>

<style>
  .card {
    transition: 0.3s;
    border-radius: 5px;
    border: 1px solid #e2e2e2;
    position: relative;
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
  .label {
    font-size: 12px;
    padding: 2px 6px;
    border-radius: 100px;
    position: absolute;
    top: 0;
    right: 0;
    margin: 12px;
    cursor: pointer;
  }
  .toread {
    color: white;
    background-color: #008cba;
    border: 2px solid #008cba;
    box-shadow: 1px 1px 0 #034f86;
  }
  .toread:active {
    background-color: #034f86;
    border: 2px solid #034f86;
  }
  .reading {
    color: white;
    background-color: #4caf50;
    border: 2px solid #4caf50;
    box-shadow: 1px 1px 0 #306532;
  }
  .reading:active {
    background-color: #306532;
    border: 2px solid #306532;
  }
  .finsihed {
    color: black;
    background-color: #e7e7e7;
    border: 2px solid #e7e7e7;
    box-shadow: 1px 1px 0 #8c8787;
  }
  .finsihed:active {
    background-color: #8c8787;
    border: 2px solid #8c8787;
  }
  .delete {
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
    <button
      class="label"
      class:toread={label === 'To Read'}
      class:reading={label === 'Reading'}
      class:finsihed={label === 'Finished'}
      on:click={updateLabel}>
      {label}
    </button>
    <img src={imageLink} alt="Thumbnail" />
    <div class="container">
      <a href={infoLink}>
        <h4>
          <b>{title}</b>
        </h4>
      </a>
      <p>{authors}</p>
    </div>
    <button class="delete" on:click={del}>❌ Delete</button>
  </div>
</li>

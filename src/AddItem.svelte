<script>
  export let name = "New Item Name";
  export let desc = "New Item Description";
  export let quantity = "1";
  export let categories = "all";

  function createItem() {
    let data = new FormData();

    let image = document.getElementById("image");

    if (typeof image.files[0] === "undefined") {
      alert("Must supply image!");
      return false;
    }

    data.append("name", name);
    data.append("description", desc);
    data.append("quantity", quantity);
    data.append("categories", categories);
    data.append("image", image.files[0]);

    fetch("https://tech-catalog-backend.fly.dev/add_item", {
      method: "POST",
      body: data,
    })
      .then((data) => data.json())
      .then((json) => console.log(json))
      .then(() => document.location.reload());
  }
</script>

<div>
  <h1 contenteditable="true" bind:textContent={name}>{name}</h1>
  <p contenteditable="true" bind:textContent={desc}>{desc}</p>
  <p contenteditable="true" bind:textContent={quantity}>{quantity}</p>
  <p contenteditable="true" bind:textContent={categories}>{categories}</p>
  <input type="file" id="image" accept="image/*" />
  <button on:click={createItem}>Create!</button>
</div>

<style>
  div {
    background-color: #f1faee;
    width: 380px;
    text-align: center;
    border-radius: 20px;
    border-style: solid;
    border-color: #459d67;
    border-width: 3px;
    padding: 1%;
    padding-top: 0;
    margin: 1%;
  }

  h1 {
    color: #e63946;
  }

  button {
    width: 95%;
    margin-top: 3%;
    background-color: #eeeeee;
    color: #459d67;
    border-radius: 20px;
  }

  p {
    color: #457b9d;
  }
</style>

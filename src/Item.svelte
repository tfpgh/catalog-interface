<script>
  import { onMount } from "svelte";
  export let key;
  export let name = "Default Name";
  export let desc = "Default Description";
  export let quantity = "1";
  export let categories = "";
  export let rotation = 0;
  export let image_url = "https://via.placeholder.com/720";

  function updateItem() {
    const item = {
      key: key,
      name: name,
      description: desc,
      quantity: quantity,
      categories: categories,
      rotation: rotation,
    };

    fetch("https://tech-catalog-backend.fly.dev/update_item", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(item),
    });
  }

  function deleteItem() {
    fetch("https://tech-catalog-backend.fly.dev/delete_item?key=" + key, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
    }).then(() => document.location.reload());
  }

  let image;
  let image_margin = 0;

  function updateRotation() {
    image.style.transform = "rotate(" + rotation * 90 + "deg)";
    if (rotation % 2 === 0) {
      image_margin = 0;
    } else {
      image_margin = (image.width - image.height) / 2;
    }
  }

  onMount(() => {
    updateRotation();
  });
</script>

<div on:input={updateItem}>
  <h1 contenteditable="true" bind:textContent={name}>{name}</h1>
  <p contenteditable="true" bind:textContent={desc}>{desc}</p>
  <p contenteditable="true" bind:textContent={quantity}>{quantity}</p>
  <p contenteditable="true" bind:textContent={categories}>{categories}</p>
  <img
    src={image_url}
    alt={desc}
    bind:this={image}
    width="364"
    height="274"
    style="margin: {image_margin}px auto;"
  />
  <button on:click={deleteItem}>Delete!</button>
  <button
    on:click={() => {
      rotation += 1;
      updateItem();
      updateRotation();
    }}
    style="color: #457b9d;">Rotate!</button
  >
</div>

<style>
  div {
    background-color: #f1faee;
    width: 380px;
    text-align: center;
    border-radius: 20px;
    border-style: solid;
    border-color: #457b9d;
    border-width: 3px;
    padding: 1%;
    padding-top: 0;
    margin: 1%;
  }

  h1,
  button {
    color: #e63946;
  }

  button {
    width: 95%;
    margin-top: 3%;
    background-color: #eeeeee;
    border-radius: 20px;
  }

  p {
    color: #457b9d;
  }

  img {
    max-width: 95%;
    border-radius: 20px;
  }
</style>

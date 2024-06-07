<script>
  import { onMount } from "svelte";
  import AddItem from "./AddItem.svelte";
  import Item from "./Item.svelte";

  let items = [];
  onMount(async () => {
    const res = await fetch(`https://tech-catalog-backend.fly.dev/get_items`);
    items = await res.json();
  });
</script>

<main>
  <AddItem />
  {#each items as item}
    <Item
      key={item.key}
      name={item.name}
      desc={item.description}
      quantity={item.quantity}
      categories={item.categories}
      rotation={item.rotation}
      image_url={"https://tech-catalog-images.s3.us-west-1.amazonaws.com/" +
        item.key +
        ".png"}
    />
  {/each}
</main>

<style>
  :global(body) {
    background-color: #eeeeee;
  }

  main {
    display: flex;
    flex-wrap: wrap;
    flex-shrink: 1;
    justify-content: center;
  }
</style>

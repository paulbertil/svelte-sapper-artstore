<script context="module">
  export async function preload() {
    const result = await this.fetch('http://localhost:1337/Products');
    const data = await result.json();
    return { products: data };
  }
</script>

<script>
  import Cart from '../../components/Cart.svelte';
  import Image from 'svelte-image';
  export let products;
</script>

<style>
  ul {
    margin: 0 0 1em 0;
    line-height: 1.5;
    list-style-type: none;
  }

  .product-listings {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 2rem;
  }

  .product-listing {
    width: 100%;
  }

  .link {
    text-transform: uppercase;
    font-weight: 700;
  }
</style>

<svelte:head>
  <title>Store</title>
</svelte:head>

<h1 class="heading-primary">Shop</h1>

<ul class="product-listings">
  <Cart />

  {#each products as product}
    <!-- we're using the non-standard `rel=prefetch` attribute to
				tell Sapper to load the data for the page as soon as
				the user hovers over the link or taps it, instead of
        waiting for the 'click' event -->

    <!-- Product listing -->
    <li class="product-listing">
      <Image src="http://localhost:1337{product.image.url}" alt="" />
      <div />
      <a
        class="link"
        rel="prefetch"
        href="store/{product.slug}">{product.title}</a>
    </li>
  {/each}
</ul>

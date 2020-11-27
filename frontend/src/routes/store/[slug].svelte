<script context="module">
  export async function preload({ params }) {
    // the `slug` parameter is available because
    // this file is called [slug].svelte
    const res = await this.fetch(
      `http://localhost:1337/products/?slug=${params.slug}`
    );
    const data = await res.json();

    if (res.status === 200) {
      return { product: data[0] };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script>
  import Image from 'svelte-image';
  export let product;
  console.log(product);
</script>

<style>
  /*
		By default, CSS is locally scoped to the component,
		and any unused styles are dead-code-eliminated.
		In this page, Svelte can't know which elements are
		going to appear inside the {{{post.html}}} block,
		so we have to use the :global(...) modifier to target
		all elements inside .content
	*/
  .product-container {
    display: flex;
  }

  @media (max-width: 800px) {
    .product-container {
      flex-direction: column;
    }
  }

  .product-image {
    width: 100%;
    max-width: 400px;
    margin-right: 2rem;
  }

  .product-info {
    max-width: 500px;
  }

  .product-price {
    font-size: 2rem;
    font-weight: 700;
  }

  .btn {
    padding: 1rem 1.5rem;
    border: none;
    border-radius: 8px;
    font-weight: 700;
    margin-top: 2rem;
    cursor: pointer;
  }

  .btn-primary {
    background-color: #000000;
    color: #ffffff;
  }
</style>

<svelte:head>
  <title>{product.title}</title>
</svelte:head>

<a href="/store">Back to all</a>

<div class="product-container">
  <div class="product-image">
    <Image src="http://localhost:1337{product.image.url}" alt={product.title} />
  </div>

  <div class="product-info">
    <h1 class="heading-primary">{product.title}</h1>
    <p class="product-price">{product.price} SEK</p>

    <h2 class="heading-secondary">Product Info</h2>
    <p class="product-description">{product.description}</p>

    <button class="btn btn-primary">Add to card</button>
  </div>
</div>

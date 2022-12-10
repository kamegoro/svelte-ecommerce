<script>
  import Slider from "./lib/Slider.svelte";
  let cart = [];
  let relatedProducts = [
    {
      id: 'react-guide',
      name: 'React Guide',
      price: 3500
    },
    {
      id: 'vue-guide',
      name: 'Vue Guide',
      price: 3500
    },
    {
      id: 'angular-guide',
      name: 'Angular Guide',
      price: 3500
    }
  ];

  let product = {
    id: 'svelte-guide',
    name: 'Svelte Guide',
    price: 3500,
    images: [
      'https://via.placeholder.com/300x424/8080ff/ffffff?text=image%201',
      'https://via.placeholder.com/300x424/80ff80/ffffff?text=image%202',
      'https://via.placeholder.com/300x424/ff8080/ffffff?text=image%203'
    ]
  };

  let sliderLeftIndex = product.images.length - 1;
  let sliderCenterIndex = 0;
  let sliderRightIndex = 1;

  function sliderMoveLeft() {
    const length = product.images.length;
    sliderLeftIndex = (sliderLeftIndex - 1 + length) % length;
    sliderCenterIndex = (sliderCenterIndex - 1 + length) % length;
    sliderRightIndex = (sliderRightIndex - 1 + length) % length;
  }

  function sliderMoveRight() {
    sliderLeftIndex = (sliderLeftIndex + 1) % product.images.length;
    sliderCenterIndex = (sliderCenterIndex + 1) % product.images.length;
    sliderRightIndex = (sliderRightIndex + 1) % product.images.length;
  }

  function addToCard(productId) {
    cart = [...cart, productId];
  }
</script>

<header class="header">
  <a class="header-title" href="/">Svelte EC</a>
  <nav>
    <ul class="header-links">
      <li>ようこそゲストさん</li>
      <li>
        <a href="/cart">カート (0)</a>
      </li>
    </ul>
  </nav>
</header>

<article class="product">
  <div class="product-main">
    <div class="silder-container">
      <Slider images={product.images} />
    </div>

    <div>
      <h2>Svelte Guide</h2>
      <dl>
        <dt>価格</dt>
        <dd>3500円</dd>
      </dl>
      <div>
        {#if !cart.includes('svelte-guide')}
          <button>カートに入れる</button>
        {:else}
          <button disabled>カード追加済み</button>
        {/if}
      </div>
    </div>
  </div>

  <footer>
    <h3>関連商品</h3>
    <ul>
      {#each relatedProducts as product}
        <li>
          <a href="/products/{product.id}">{product.name}</a>
          - {product.price}円
        </li>
      {/each}
    </ul>
  </footer>
</article>

<style>
  :global(body) {
    margin: 0;
    background-color: #eee;
    padding: 0;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    background-color: #fff;
    padding: 0 15px;
    width: 100%;
    max-width: 800px;
    height: 50px;
  }

  .header-title {
    font-weight: bold;
  }

  .header-links {
    display: flex;
    gap: 10px;
    margin: 0;
    padding: 0;
    list-style: none;
  }

  .product {
    margin: 0 auto;
    background-color: #fff;
    padding: 15px;
    width: 100%;
    max-width: 800px;
  }

  .product-main {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .silder-container {
    width: 100%;
    max-width: 400px;
    overflow: hidden;
  }
</style>
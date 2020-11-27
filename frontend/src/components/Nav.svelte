<script>
  export let segment;
</script>

<style>
  .navbar {
    border-bottom: 1px solid rgba(0, 0, 0, 0.12);
  }

  .navbar-container {
    display: flex;
    align-content: center;
    justify-content: space-between;
    max-width: 1400px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  @media (max-width: 700px) {
    .navbar-container {
      flex-direction: column;
    }
  }

  .logo {
    display: flex;
    align-items: center;
    justify-content: center;
    text-transform: uppercase;
    font-weight: 900;
  }

  .logo .circle {
    width: 20px;
    height: 20px;
    background-color: #000000;
    border-radius: 50%;
    margin-right: 0.2rem;
  }
  .logo a {
    display: flex;
    align-items: center;
  }

  nav {
    font-weight: 300;
    padding: 0 1em;
    display: flex;
    justify-content: center;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  /* clearfix */
  ul::after {
    content: '';
    display: block;
    clear: both;
  }

  li {
    display: block;
    float: left;
  }

  li:not(:last-of-type) {
    margin-right: 2rem;
  }

  [aria-current] {
    position: relative;
    display: inline-block;
  }

  [aria-current]::after {
    position: absolute;
    content: '';
    width: calc(100% - 1em);
    height: 2px;
    background-color: #000000;
    display: block;
    bottom: -1px;
  }

  a {
    text-decoration: none;
    padding: 1em 0.5em;
    display: block;
    text-transform: uppercase;
  }
</style>

<div class="navbar">
  <div class="navbar-container">
    <div class="logo">
      <a href="/">
        <div class="circle" />
        The Store</a>
    </div>

    <nav>
      <ul>
        <li>
          <a
            aria-current={segment === undefined ? 'page' : undefined}
            href=".">Selected Works</a>
        </li>
        <li>
          <a
            rel="prefetch"
            aria-current={segment === 'store' ? 'page' : undefined}
            href="store">store</a>
        </li>
        <li>
          <a
            aria-current={segment === 'about' ? 'page' : undefined}
            href="about">about</a>
        </li>
        <!-- for the blog link, we're using rel=prefetch so that Sapper prefetches
           the blog data when we hover over the link or tap it on a touchscreen -->

        <li>
          <a
            rel="prefetch"
            aria-current={segment === 'cart' ? 'page' : undefined}
            href="cart">cart</a>
        </li>
      </ul>
    </nav>
  </div>
</div>

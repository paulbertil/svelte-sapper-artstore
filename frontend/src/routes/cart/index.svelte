<script>
  import { onMount } from 'svelte';

  let stripeReady = false;
  let mounted = false;

  onMount(async () => {
    mounted = true;
    console.log('hi');
    if (stripeReady) {
      loadStripeElements();
    }
  });

  function stripeLoaded() {
    stripeReady = true;
    if (mounted) {
      loadStripeElements();
    }
  }

  function loadStripeElements() {
    const stripe = new Stripe('pk_test_rdW6s8iBpSDJYI7aeUVkFtfY00iYnnPo7R');
    var elements = stripe.elements();

    console.log(elements);
    var style = {
      base: {
        padding: '10px 12px',
        color: '#32325d',
        fontFamily:
          '-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif',
        fontSmoothing: 'antialiased',
        fontSize: '16px',
        '::placeholder': {
          color: '#aab7c4',
        },
      },
      invalid: {
        color: '#fa755a',
      },
    };
  }
</script>

<svelte:head>
  <title>Cart</title>
  <script src="https://js.stripe.com/v3/" on:load={stripeLoaded()}>
  </script>
</svelte:head>

<h1>Cart Page</h1>

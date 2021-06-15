# Headless Checkout

<div class="otp" id="no-index">

### On this Page

- [Redirecting to the BigCommerce checkout](#redirecting-to-the-bigcommerce-checkout)
- [Embedding the BigCommerce checkout](#embedding-the-bigcommerce-checkout)
- [Using the checkout API](#using-the-checkout-api)
- [Other checkout options](#other-checkout-options)
- [Next steps](#next-steps)
- [Resources](#resources)

</div>

In this article we'll walk through how to embed BigCommerce's checkout into an iFrame on a headless site. At the end of this article, we'll list out some other checkout options for headless users.

## Redirecting to the BigCommerce checkout



## Embedding the BigCommerce checkout

If the shopper is a guest (and the cart is a guest cart)

* Generate embedded checkout URL from cart API, use this URL for checkout SDK

If the shopper is a customer (and they're already signed in to the headless storefront, so you created the cart with their customer ID)

* Generate embedded checkout URL from cart API
* Create a customer login JWT using the customer ID, and set the redirect_to parameter to the relative URL of the embedded checkout URL (essentially wrapping the checkout URL in a login URL)
* Pass this new URL to checkout SDK, which will ensure the customer is logged in before the checkout is loaded

This customer login JWT must also include a `channel_id` property, which is currently undocumented. If this channel ID is not included, CORS checks will fail and the checkout won't load.

[Learn more about Embedded Checkout](https://developer.bigcommerce.com/api-docs/storefronts/embedded-checkout/embedded-checkout-tutorial).

## Using the checkout API

## Other checkout options

* [Redirect to BigCommerce's hosted checkout using the Server-to-Server Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api)
* [Create custom BigCommerce hosted checkout pages from scratch using Checkout SDK](https://developer.bigcommerce.com/stencil-docs/customizing-checkout/checkout-sdk-quickstart).
* [Create a custom BigCommerce hosted checkout from a fork of BigCommerce's Checkout-JS](https://github.com/bigcommerce/checkout-js).
* [Build a custom checkout experience from scratch using the Server-to-Server Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api).
* [Restyle the BigCommerce hosted checkout](https://developer.bigcommerce.com/stencil-docs/customizing-checkout/optimized-one-page-checkout).

## Next steps

* [Learn more about {{TOPIC}}]().

## Resources

* [Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts)
* [Checkouts API](https://developer.bigcommerce.com/api-reference/store-management/checkouts)
* [Embedded Checkout Tutorial](https://developer.bigcommerce.com/api-docs/storefronts/embedded-checkout/embedded-checkout-tutorial)
# Handling Checkout

<div class="otp" id="no-index">

### On this Page	
- [Headless checkout options](#headless-checkout-options)
- [Next steps](#next-steps)
- [Resources](#resources)

</div>

Introduction

## Headless checkout options

* [Embed BigCommerce's checkout in an iFrame with Embedded Checkout](https://developer.bigcommerce.com/api-docs/storefronts/embedded-checkout/embedded-checkout-overview).
* [Redirect to BigCommerce's hosted checkout using the Server-to-Server Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api)
* [Create custom BigCommerce hosted checkout pages from scratch using Checkout SDK](https://developer.bigcommerce.com/stencil-docs/customizing-checkout/checkout-sdk-quickstart).
* [Create a custom BigCommerce hosted checkout from a fork of BigCommerce's Checkout-JS](https://github.com/bigcommerce/checkout-js).
* [Build a custom checkout experience from scratch using the Server-to-Server Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api).
* [Restyle the BigCommerce hosted checkout](https://developer.bigcommerce.com/stencil-docs/customizing-checkout/optimized-one-page-checkout).
* [Process payments using the Payments API](https://developer.bigcommerce.com/api-reference/payments/payments-process-payments).

## Redirect to a BigCommerce checkout

When creating a cart, there is an optional query to create a redirect URL. Use this to redirect the shopper to a BigCommerce hosted checkout page.

If you are using the hosted checkout option, shoppers will be able to navigate to other pages of the store. Here's a few methods to prevent this:

1. Use BigCommerce's [Sites and Routes API](https://developer.bigcommerce.com/api-reference/cart-checkout/sites-routes-api) to create redirects from BigCommerce hosted pages back to the non-BigCommerce storefront (recommended).
2. Hide non essential pages by removing the back links in Cart and Checkout
3. Add a JavaScript redirect on all pages (except `/checkout`) that redirects to the non-BigCommerce storefront
4. Wrap all content in the theme's layouts in a conditional that only renders the BC storefront if certain conditions are met (like an admin customer group, for example), and redirect to the non-BigCommerce storefront otherwise.
5. Replace all content in theme layout files with a redirect to the non-BigCommerce storefront

To customize the checkout when using a redirect URL, use our [Checkout SDK](https://github.com/bigcommerce/checkout-sdk-js). The Checkout JS SDK is a library of methods for interacting with the checkout page's underlying Storefront Checkout API, allowing you to build a custom checkout page UI in the framework of your choice.

## Checkout API

If you need complete control over the checkout page, you have the option to build an external checkout in your CMS or app using the server-to-server Checkout API. Then use the Payments API to process a payment through BigCommerce to take payment for the order. If you are using the Payments API, you are responsible for [PCI compliance](#pci-compliance).

## Next steps
* [Learn more about {{TOPIC}}]().

## Resources
* [Link]() 
<div class="otp" id="no-index">

### On this Page	
- [Storefronts](#storefronts)
- [Storefront Carts](#storefront-carts)
- [Storefront Orders](#storefront-orders)
- [Storefront Checkouts](#storefront-checkouts)
	
</div>
<br>

## Storefronts
BigCommerce’s Storefront API exposes storefront data to Stencil themes. You can use this client API to manage a shopper’s cart, checkout, and order data via client-side JavaScript.

## Storefront Carts
The Storefront Cart does not use API Tokens and allows for cart data to be scraped directly from the front end or used in a Stencil Theme.

Notes:

- The Try It Now at each endpoint will not work. Please see Cart and Checkout for a script that can be used to get Cart details.
- `cartId` is the same as the `checkoutId`.
- Carts are valid for 30 days after the last modification. A modification includes the initial cart creation or editing the existing cart.
- Redirect URLs can be generated only from carts created using the server-to-server cart API. To restore a cart that was created on the storefront–either by a shopper or the Storefront Cart API–first recreate the cart using the server-to-server Cart API.

By default, the cart response will return abbreviated details for cart line items. To get full details of selected product options, use the following query parameters:

- Physical products only: ?include=lineItems.physicalItems.options
- Digital products only: ?include=lineItems.digitalItems.options
- Both physical and digital items: `?include=lineItems.digitalItems.options,lineItems.physicalItems.options`

## Storefront Orders

## Storefront Checkouts

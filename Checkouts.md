<div class="otp" id="no-index">

### On this Page	
- [Section1](#section1)
- [Section2](#section2)
- [Section3](#section3)

</div>
<br>

**Server-to-Server APIs**

The Server-to-Server APIs are for managing the contents of a shopping cart and checkout remotely, from a server.

**Storefront APIs**

The Storefront APIs are for managing the contents of a shopper’s cart and checkout using JavaScript in the context of a storefront session.

BigCommerce’s Storefront API exposes storefront data to Stencil themes. You can use this client API to manage a shopper’s cart, checkout, and order data via client-side JavaScript.

The Storefront Checkout does not use API Tokens and allows for Checkout data to be scraped directly from the front end or used in a Stencil Theme.

## Checkouts

Allows for a checkout to be created from an existing cart using BigCommerce checkout logic. The existing BigCommerce front end cart/checkout can be bypassed.

**Notes:** `checkoutId` is the same as `cartId`.

Resource / Endpoint|Description|
|-|-|
|[`Get a Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout/checkoutsbycheckoutidget)|Returns a Checkout|
|[`Update Customer Messages`](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api/checkout/checkoutsbycheckoutidput)|Updates Checkout customer messages (**Storefront API**)|

## Checkouts Billing Address

Resource / Endpoint|Description|
|-|-|
|[`Add Checkout Billing Address`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost)|Adds a billing address to a Checkout|
|[`Update Checkout Billing Address`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a billing address on a Checkout|

## Checkouts Consignments

A consignment consists of a shipping address with the associated line items. At a minimum, one shipping address with line items and shipping options must be included in the checkout. If multiple shipping locations are used, match each lineItem with the correct shipping address. When adding a shipping address to the checkout, include the ?include=consignments.availableShippingOptions query parameter to return the shipping options available for any address.

**Note:** Only one consignment can be updated at a time. 

Resource / Endpoint|Description|
|-|-|
|[`Add Consignment to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost)|Adds a new Consignment to Checkout|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a Consignment|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidandconsignmentiddelete)|Deletes a Consignment from Checkout|

## Checkouts Coupons
Resource / Endpoint|Description|
|-|-|
|[`Add Coupon to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-coupons/checkoutscouponsbycheckoutidpost)|Adds a Coupon Code to Checkout|
|[`Delete Checkout Coupon`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-coupons/checkoutscouponsbycheckoutidandcouponcodedelete)|Deletes a Coupon Code from Checkout|

## Checkouts Orders

Orders created will be set to incomplete order status.

You can create as many orders from the same order(cart) as you want. Order duplication creates the same order with a new order number with the incomplete status. Once the order is paid, then the cart is deleted. Cart deletion occurs if you are using BigCommerce to accept payments on orders.

Resource / Endpoint|Description|
|-|-|
|[`Create an Order`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-orders/createanorder)|Creates an Order|

## Checkout Cart Items (Storefront API)

**Notes:**
* If a variant needs to be changed or updated, the product will need to be removed and re-added to the cart with the correct variants using the [Add Cart Line Items](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-cart-api/cart-items/addcartlineitem) endpoint.

Resource / Endpoint|Description|
|-|-|
|[`Update a Line Item`](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api/checkout-cart-items/checkoutscartsitemsitemidbycheckoutidandcartidput)|Updates a Checkout Line Item|
|[`Delete a Line Item`](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api/checkout-cart-items/checkoutscartsitemsitemidbycheckoutidandcartiddelete)|Deletes a Line Item from the Cart|

## Checkout Gift Certificates (Storefront API)

Resource / Endpoint|Description|
|-|-|
|[`Add Gift Certificate to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api/checkout-gift-certificates/checkoutsgiftcertificatesbycheckoutidpost)|Adds a Gift Certificate Code to Checkout|
|[`Delete Gift Certificate`](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api/checkout-gift-certificates/checkoutsgiftcertificatesbycheckoutidandgiftcertificatecodedelete)|Deletes a Gift Certificate|

### Troubleshooting Checkout Errors




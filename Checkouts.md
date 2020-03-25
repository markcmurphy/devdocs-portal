<div class="otp" id="no-index">

### On this Page	
- [Section1](#section1)
- [Section2](#section2)
- [Section3](#section3)

</div>
<br>

The Server-to-Server APIs are for managing the contents of a shopping cart and checkout remotely, from a server.

## Checkouts

Allows for a checkout to be created from an existing cart using BigCommerce checkout logic. The existing BigCommerce front end cart/checkout can be bypassed.

**Notes:** `checkoutId` is the same as `cartId`.

Resource / Endpoint|Description|
|-|-|
|[`Get a Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout/checkoutsbycheckoutidget)|Returns a Checkout|

## Checkouts Billing Address

Resource / Endpoint|Description|
|-|-|
|[`Add Checkout Billing Address`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost)|Adds a billing address to a Checkout|
|[`Update Checkout Billing Address`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a billing address on a Checkout|

## Checkouts Consignments

Resource / Endpoint|Description|
|-|-|
|[`Add Consignment to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost)|Adds a new Consignment to Checkout|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a Consignment|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidandconsignmentiddelete)|Deletes a Consignment from Checkout|

## Checkouts Coupons

## Checkouts Orders

## Checkout Cart Items

## Checkout Gift Certificates

### Troubleshooting Checkout Errors




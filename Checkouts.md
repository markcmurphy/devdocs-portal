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

## Checkout Cart Items

Resource / Endpoint|Description|
|-|-|
|[`Add Consignment to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost)|Adds a new Consignment to Checkout|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a Consignment|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidandconsignmentiddelete)|Deletes a Consignment from Checkout|

## Checkout Gift Certificates

Resource / Endpoint|Description|
|-|-|
|[`Add Consignment to Checkout`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost)|Adds a new Consignment to Checkout|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidandaddressidput)|Updates a Consignment|
|[`Update Checkout Consignment`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidandconsignmentiddelete)|Deletes a Consignment from Checkout|

### Troubleshooting Checkout Errors




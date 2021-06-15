# Create an order from a cart

<div class="otp" id="no-index">

### On this page

- [Create a cart](#create-a-cart)
- [Add a billing address](#add-a-billing-address)
- [Add a consignment](#add-a-consignment)
- [Update consignment with shipping options](#update-consignment-with-shipping-options)
- [Create the order](#create-the-order)
- [Resources](#resources)

</div>

In this tutorial, we'll use the Cart and Checkout APIs to create an order.

## Create a cart

Create a [Cart](/api-reference/cart-checkout/server-server-cart-api/cart/createacart) with a redirect url
* Add the Customer ID or leave blank if shopper is a guest
* Add Line Items or Custom Line Items

## Add a billing address

Add a [Billing Address](/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost) to the [Cart](/api-reference/cart-checkout/server-server-cart-api/cart/createacart) changing it to a Checkout

## Add a consignment

Add a [Consignment](/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost) to Checkout with the line items and the `consignments.available_shipping_options` query

## Update consignment with shipping options

Update each [Consignment](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments) with the chosen shipping option from the Add Consignment response.

## Create the order

Create the Order by sending a request to [Create Order](/api-reference/cart-checkout/server-server-checkout-api/checkout/createanorder)
* Returns an `order_id`
* Order is created in `incomplete` status

## Resources

* [Link]()

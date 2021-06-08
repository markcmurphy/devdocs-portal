# Processing Orders

<div class="otp" id="no-index">

### On this Page	
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

Introduction

## Sending order confirmation emails

Content

## Section2
Content

## Section3
Content

## Section4
Content

## Samples

### Creating orders from a cart

1.  Create a [Cart](/api-reference/cart-checkout/server-server-cart-api/cart/createacart) with a redirect url
	1.  Add the Customer ID or leave blank if shopper is a guest
	2.  Add Line Items or Custom Line Items
2.  Add a [Billing Address](/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost) to the [Cart](/api-reference/cart-checkout/server-server-cart-api/cart/createacart) changing it to a Checkout
3.  Add a [Consignment](/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost) to Checkout with the line items and the `consignments.available_shipping_options` query
4. Update each [Consignment](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments) with the chosen shipping option from the Add Consignment response.
5.  Create the Order by sending a request to [Create Order](/api-reference/cart-checkout/server-server-checkout-api/checkout/createanorder)
	1.  Returns an `order_id`
	2. Order is created in `incomplete` status
6.  Take a Payment for the Order using one of the two methods below

### Create an Order Directly

1.  Send a request /POST request to [Orders](/api-reference/orders/orders-api/orders/createanorder)
	1. Make sure the `status_id` is 0
	2.  Add the Customer ID or leave blank if the shopper is a guest
	3. Add Line Items or Custom Line Items
	4. Add a Billing Address
	5. Add a Shipping Address
	6. Create a custom shipping quote
2.  Take a Payment for the Order using one of the two methods below
3.  Vaulted Card -- The shopper has saved a credit card
	1. [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget)
	2.  [Create Access Token](/api-reference/payments/payments-create-payment-token-api/payment-access-token/paymentsaccesstokenspost)
	3.  [Process Payment](/api-reference/payments/payments-process-payments/payment/paymentspost)
4.  Credit Card -- The shopper has not saved a credit card
	1. [Create Access Token](/api-reference/payments/payments-create-payment-token-api/payment-access-token/paymentsaccesstokenspost)
	2. [Process Payment](/api-reference/payments/payments-process-payments/payment/paymentspost)

## Next Steps
* [Learn more about {{TOPIC}}]().

## Resources
* [Link]() 
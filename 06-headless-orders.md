# Processing Orders

<div class="otp" id="no-index">

### On this Page	
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

Introduction

## Creating orders from a cart


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
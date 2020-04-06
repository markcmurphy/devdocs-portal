# Payments

<div class="otp" id="no-index">

### On this Page
- [Payments API](#payments-api)
- [Payment Methods (Enabled on Store)](#payment-methods-enabled-on-store)
- [Payment Processing Methods (On Order)](#payment-processing-methods-on-order)
- [Payment Processing Token](#payment-processing-token)
- [Error Codes](#error-codes)
- [FAQ](#faq)
- [Resources](#resources)


</div>

## Payments API


## Payment Methods (Enabled on Store)
v2
Returns a list of all enabled Payment Methods on a store. If you are trying to process payment for an order see Payments API.

## Payment Processing Methods (On Order)
Depending on merchant’s configuration in BigCommerce’s Control Panel, the payment request will be processed as either ‘Authorize only’ or ‘Authorize and Capture’.

Payments can be processed using Stored Cards, Payment Tokens or Credit Cards.

## Payment Processing Token
This endpoint provides the capability to create a payment access token. The payment access token is required when making request to Payment API for submitting payment for an order.

## Error Codes

| Code | Description | Possible Causes | Possible Solutions |
|-|-|  - |  - |
| `10000` |  An internal error has occurred within the API. |  Connection error | Try the request again. |
| `10001` | Missing or incorrect required fields. | Missing or Incorrect Fields |  Check the request for any data that is incorrect or is missing |
| `30000` | Merchant payment configuration could not be found. | * The payment provider has not been configured in the store. | Check the [payment gateways](https://support.bigcommerce.com/s/article/Online-Payment-Methods#setup) settings in your BigCommerce store. |
| `3001` | Merchant payment configuration is not correctly being configured. | The payment configuration is being rejected by the payment gateway. | Check the [payment gateways](https://support.bigcommerce.com/s/article/Online-Payment-Methods#setup) settings in your BigCommerce store. <br> Reach out the the payment gateway to check the information is correct. |
| `30002` | Vaulting service is currently not available. |  The vaulting feature is not enabled on this store. | Reach out to the store owner to enable [Stored Credit Cards](https://support.bigcommerce.com/s/article/Enabling-Stored-Credit-Cards) |
| `30003` | Order could not be found. | The order does not exist. <br> The order ID is not correct. |  Check the current orders in the store using [Get All Orders](https://developer.bigcommerce.com/api-reference/orders/orders-api/orders/getanorder) |
| `30004` | The validation on line item and grand total does not match. | N/A| Recreate the payment access token <br> Recreate the order <br> Ensure the store settings for taxes and discounts are setup correctly|
| `30050` | Payment instrument could not be saved. | Credit card information is incorrect. | Check that the card information is correct.<br> * `expiry_month` is two digits<br>* `expiry_year` is four digits |
| `30051` | The stored card was not found. |  The card requested for payment is not associated to the shopper.| Use [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget) to see available vaulted cards |
|`30100` | Payment access token could not be created. | N/A|N/A|
| `30101` | Order is invalid. | The order is in the wrong status. | Orders must be in Incomplete Status with a `status_id:0` <br>  The order must be created by the Checkout SDK, Checkout API or V2 Orders API. Orders created in the Control and set to an incomplete status will return this error. |
| `30102` | The payment was declined. | The card information provided was incorrect<br>The token provided was incorrect | Check that the provider shopper information is correct<br>Make sure the token in the Authorization header field is correct |
| `30103` | Card has expired |N/A | N/A|
| `30104` | The payment was declined. Please contact card issuer for more information. |N/A |N/A|
| `30105` | The payment was declined due to duplicate payment being submitted. |N/A |N/A |
| `30106` | The payment was declined due to insufficient funds. |N/A |N/A|

## FAQ

**How do I get a list of stored credit cards?**
Use the Get Payment Methods to get a list of stored payment instruments. 

**Can I add my payment gateway?**
The Payments API does not support adding a third party gateway. Payments are processed through BigCommerce.

**Can I issue a refund?**
Refunds can be issued either using the [Control Panel](https://support.bigcommerce.com/s/article/Processing-Refunds) or through the payment gateway directly.

**How do I process payment for a capture credit card?**
Once a payment has been authorized, the capture step will need to be completed using the [Control Panel](https://support.bigcommerce.com/s/article/How-can-I-set-my-payment-gateway-to-only-authorize-transactions-and-not-capture-the-funds-automatically).

**Can I use this on orders with more than one shipping address?**
Yes, checkouts and orders with more than one consignment can use the Payments API.

**Is store credit supported?**
Store credit is not a supported payment method with the Payments API. Store credit can still be used by the shopper on the storefront, part of the control panel or with the Checkout API.

**Are gift certificates supported?**
The Payment Processing API is for processing payments through a store's payment gateway. Since BigCommerce store gift cards are not processed through a payment gateway, they can not be processed through via the Payment Processing API.

**Are offline payment methods supported?**
The Payments API is designed to process credit card payments through supported payment gateways; it does not expose methods for processing [offline payment methods](https://support.bigcommerce.com/s/article/Offline-Payment-Methods) such as cash on delivery.

## Resources

### Webhooks
- [Customer Payment Instrument](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_customer)
- [Orders](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_orders)
- [Cart](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_cart)

### Related Endpoints
* [Create Access Token](/api-reference/payments/payments-create-payment-token-api/payment-access-token/paymentsaccesstokenspost)
* [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget)
* [Process Payment](/api-reference/payments/payments-process-payments/payment/paymentspost)

### Related Articles
* [Enabling Stored Credit Cards](https://support.bigcommerce.com/s/article/Enabling-Stored-Credit-Cards) (BigCommerce Support)
* [Processing Refunds](https://support.bigcommerce.com/s/article/Processing-Refunds) (BigCommerce Support)
* [Manually Capturing Transactions (Authorize Only)](https://support.bigcommerce.com/s/article/How-can-I-set-my-payment-gateway-to-only-authorize-transactions-and-not-capture-the-funds-automatically) (BigCommerce Support)
* [Available Payment Gateways](https://support.bigcommerce.com/s/article/Available-Payment-Gateways) (BigCommerce Support)
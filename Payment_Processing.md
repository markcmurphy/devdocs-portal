# Payment Processing

<div class="otp" id="no-index">

### On this Page
- [Payment Processing Overview](#payment-processing-overview)
- [Getting Accepted Payment Methods](#getting-accepted-payment-methods)
- [Obtaining a Payment Access Token](#obtaining-a-payment-access-token)
- [Process the Payment](#process-the-payment)
  - [PAT](#pat)
- [Saving Payment Methods](#saving-payment-methods)
- [Sample App Diagram](#sample-app-diagram)
- [Supported Payment Gateways](#supported-payment-gateways)
- [PCI Compliance](#pci-compliance)
- [Usage Notes](#usage-notes)
- [FAQ](#faq)
- [Resources](#resources)
  - [Webhooks](#webhooks)
  - [Related Endpoints](#related-endpoints)
  - [Related Articles](#related-articles)


</div>

The Payment Processing API and supporting V3 REST API endpoints enable you to process payments through the store's connected payment gateway. A payment can be taken for an order that is created using either the Server to Server Checkout API Orders endpoint or creating an order using V2 Orders endpoint.

Payments are processed via a sequence of requests to two API hosts:
* Create the payment token:   `https://api.bigcommerce.com/stores/{store_hash}/v3/payments/access_tokens`
* Process the payment:   `https://payments.bigcommerce.com/stores/{store_hash}/payments`

**Requirements for Stored Cards**
* Plus plan or higher.
* Optimized One-Page Checkout.
* Compatible payment gateway.

## Payment Processing Overview
There's three steps to processing payments:
1. [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget)
2. [Create Access Token](/api-reference/payments/payments-create-payment-token-api/payment-access-token/paymentsaccesstokenspost)
3. [Process Payment](/api-reference/payments/payments-process-payments/payment/paymentspost)

## Getting Accepted Payment Methods

To get a list of accepted payment methods, make a `GET` request to `/stores/{{STORE_HASH}}/v3/payments/methods`:

```http
GET https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/payments/methods?order_id={{ORDER_ID}}
X-Auth-Token: {{ACCESS_TOKEN}}
X-Auth-Client: {{CLIENT_ID}}
Content-Type: application/json
Accept: application/json
```
[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget#requestrunner)

**Response:**

```json
{
  "data": [
    {
      "id": "stripe.card",
      "name": "Stripe",
      "test_mode": true,
      "type": "card",
      "supported_instruments": [
        {
          "instrument_type": "VISA",
          "verification_value_required": true
        },
        {
          "instrument_type": "MASTERCARD",
          "verification_value_required": true
        },
        {
          "instrument_type": "AMEX",
          "verification_value_required": true
        },
        {
          "instrument_type": "DISCOVER",
          "verification_value_required": true
        },
        {
          "instrument_type": "JCB",
          "verification_value_required": true
        },
        {
          "instrument_type": "DINERS_CLUB",
          "verification_value_required": true
        },
        {
          "instrument_type": "STORED_CARD",
          "verification_value_required": true
        }
      ],
      "stored_instruments": [
        {
          "type": "stored_card",
          "brand": "VISA",
          "expiry_month": 9,
          "expiry_year": 2020,
          "issuer_identification_number": "424242",
          "last_4": "4242",
          "token": "050a1e5c982e5905288ec5ec33f292772762033a070a45g434qfb16bf1940b51ef",
          "is_default": true
        }
      ]
    }
  ],
  "meta": {}
}
```

To pay with a stored card, first make a call to [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget) for the `stored_instruments > token`. The `order_id` is passed in as a query parameter.

This token is the same as `payment_instrument_token` from [Get Transactions](https://developer.bigcommerce.com/api-reference/orders/orders-transactions-api).

Make note of the `token` to use as part of processing the payment in the request body.

## Obtaining a Payment Access Token
2. Make a request to [Create Access Token](/api-reference/payments/payments-create-payment-token-api/payment-access-token/paymentsaccesstokenspost) to get the authorization token that needs to be passed in the header when processing the payment. The ID of the order needs to be part of the request body.

<!--
title: "Sample Request"
subtitle: "Create Payment Access Token"
lineNumbers: true
-->

**Example Request Create Payment Access Token**
`/POST https://api.bigcommerce.com/stores/{{store_hash}}/v3/payments/access_tokens`

```json
{
  "order": {
    "id": 215
  }
}
```

<!--
title: "Sample Response"
subtitle: "Create Payment Access Token"
lineNumbers: true
-->

**Example Response Create Payment Access Token**

```json
{
  "data": {
    "id": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NTEzOTQxNDIsIm5iZiI6MTU1MTM5MDU0MiwiaXNzIjoicGF5bWVudHMuYmlnY29tbWVyY2UuY29tIiwic3ViIjoianJhaDZnbW4iLCJqdGkiOiI3Nzg3ZmU1Zi01OWJmLTQ3ZWMtYTFmZC00ZDQ3ZTkwNjFlNWMiLCJpYXd4gJ8uHDk3kDhhuyefsrtr45mRhdGEiOnsic3RvcmVfaWQiOjEwMjU2NDYsIm9yZGVyX2lkIjoyMTUsImFtb3VudCI6OTgwMCwiY3VycmVuY3kiOiJVU0QifX0.WbR90d8m4gn8wK7kPMDEoVq8B0hHC5Ul5H4Hpqq6Yvo"
  },
  "meta": {}
}
```

## Process the Payment
3. To process the payment, send a POST to [Process Payment](/api-reference/payments/payments-process-payments/payment/paymentspost). You will need the following information from [Get Payment Methods](/api-reference/payments/payments-create-payment-token-api/payment-methods/paymentsmethodsget) in step one.

**Get Payment Methods = Process Payment**
* type = type
* token = token
* last_four = verfication_value
* id = payment_method_id

The headers to process a payment are different than the headers you normally send with a BigCommerce API. The Authorization token is the ID that is returned in Get Payment Access Token (step two).

**Headers**
* Accept: application/vnd.bc.v1+json
* Authorization: PAT {your-access-token}
* Content-Type: application/json

<div class="HubBlock--callout">
<div class="CalloutBlock--warning">
<div class="HubBlock-content">

<!-- theme: warning -->

### PAT
> There is a space between PAT {your-access-token}.

</div>
</div>
</div>

<!--
title: "Sample Request"
subtitle: "Process Payment"
lineNumbers: true
-->

**Example Request Process Payment**
`/POST https://payments.bigcommerce.com/stores/{store_hash}/payments`

```curl
curl -X POST \
  https://payments.bigcommerce.com/stores/{store_hash}/payments \
  -H 'Accept: application/vnd.bc.v1+json' \
  -H 'Authorization: PAT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NTEzOTQxNDIsIm5iZiI6MTU1MTM5MDU0MiwiaXNzIjoicGF5bWVudHMuYmlnY29tbWVyY2UuY29tIiwic3ViIjoianJhaDZnbW4iLCJqdGkiOiI3Nzg3ZmU1Zi01OWJmLTQ3ZWMtYTFmZC00ZDQ3ZTkwNjFlNWMiLCJpYXQiOjE1NTEzOTA1NDIsImRhdGEiOnsic3RvcmVfaWQiOjEwMjU2NDYsIm9yZGVyX2lkIjoyMTUsImFtb3VudCI6OTgwMCwiY3VycmVuY3kiOiJVU0QifX0.WbR90d8m4gn8wK7kPMDEoVq8B0hHC5Ul5H4Hpqq6Yvo' \
  -H 'Content-Type: application/json' \
  -d '{
  "payment": {
    "instrument": {
      "type": "stored_card",
      "token": "050a1e5c982e5905288ec5ec33f292772762033a0704f46fccb16bf1940b51ef", // from Get Payment Methods
      "verification_value": "4242"
    },
    "payment_method_id": "stripe.card"
  }
}'

```

<!--
title: "Sample Response"
subtitle: "Process Payment"
lineNumbers: true
-->

**Example Response Process Payment**

```json
{
  "data": {
    "id": "693bb4cd-3f20-444a-8315-6369f582c68a",
    "status": "success",
    "transaction_type": "purchase"
  }
}
```

If the purchase was successful it will return a status of success. The order is then automatically moved to an Awaiting Fulfillment status. If you get a different response, see [Error Codes](#error-codes) for troubleshooting.






## Saving Payment Methods

To store a customer's payment payment method, set `save_instrument` to `true` when processing a payment via POST to `/stores/{store_hash}/payments` :

```json
{
  "payment": {
    "instrument": {...},
    "payment_method_id": "authorizenet.card",
    "save_instrument": true
  }
}
```

**Note**: Stored payment methods must be enabled in **Store Setup › Payments > Payment Gateway**. Not all payment gateways support storing payment methods.
 For more on enabling stored cards and other payment methods, see [Enabling Stored Credit Cards](https://support.bigcommerce.com/s/article/Enabling-Stored-Credit-Cards).

## Sample App Diagram

The following diagram shows how the payment_access_token interacts with BigCommerce API and BigCommerce payments.

![](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Payments%20API%20sequence%20diagram.png)

## Supported Payment Gateways

| Supported Payment Gateways  | Stored Cards Supported |
| --------------------------- |------------------------|
| AdyenV2                     | Yes                    |
| Authorize.net               | Yes                    |
| CardConnect                 | No                     |
| Chase Integrated Payments   | No                     |
| Chase Merchant Services     | No                     |
| Cybersource Direct          | Yes                    |
| eWAY Rapid                  | No                     |
| First Data Payeezy Gateway  | No                     |
| Heartland Payment Systems   | No                     |
| MIGS                        | No                     |
| MyVirtualMerchant           | No                     |
| NMI                         | No                     |
| Paymetric                   | Yes                    |
| PayPal powered by Braintree | Yes                    |
| PayPal Payflow Pro UK       | No                     |
| PayPal Payflow Pro US       | No                     |
| QuickBooks Payments         | No                     |
| Sage Pay/Protx VSP Direct   | No                     |
| SecureNet                   | No                     |
| Stripe                      | Yes                    |
| USA ePay                    | No                     |
| Worldpay Core               | No                     |
| WorldPay                    | No                     |

**Note:** The Payment Processing API does not support hosted / offsite providers (such as PayPal or Adyen) and wallet type payments (such as Amazon Pay).

## PCI Compliance

BigCommerce is only responsible for the security of credit card to the extent that it is directly in the route of the payment request to payment processors during a payment processing request. To ensure secure handling of payment instruments, as a third-party developer, you are responsible for developing the storefronts or recurring billing apps in a PCI compliant manner and maintaining a PCI compliance certification for third-party service providers certified by an external Qualified Security Assessor (QSA).

Merchants or shoppers personal identifiable information (PII) collected by recurring billing apps that consumes the BigCommerce Payments API must have it’s own Privacy Policy sufficient to the requirements of the European Union General Data Protection Requirements (GDPR) which must be available and displayed to the general public.

**Note**: Applications that handle credit card data must be be PCI Compliant. SAQs (self-assessment questionnaires) can be submitted to
[compliance@bigcommerce.com](mailto:compliance@bigcommerce.com).

## Usage Notes

* Depending on merchant's configuration in BigCommerce's Control Panel, the payment request will be processed as either `Authorize only` or `Authorize and Capture`.
* Payments can be processed using the follow:
  1. Payment Tokens
  1. Credit Cards
  1. Stored Credit Cards

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
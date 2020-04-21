# Orders

<div class="otp" id="no-index">

### On this Page	
- [Orders](#orders)
- [V2 and V3](#v2-and-v3) 
- [Order Products](#order-products)
- [Order Status](#order-status)
- [Order Shipping Addresses](#order-shipping-addresses)
- [Order Shipping Addresses Quotes](#order-shipping-addresses-quotes)
- [Order Taxes](#order-taxes)
- [Order Coupons](#order-coupons)
- [Order Shipments](#order-shipments)
- [Order Messages](#order-messages)
- [Order Currency Fields](#order-currency-fields)
- [Order Transactions](#order-transactions)
- [Order Payment Actions](#order-payment-actions)
- [Order Returns](#order-returns)


</div>

## Orders
The Order object contains a record of the purchase agreement between a shopper and a merchant. Orders contain information about the shopper, the item(s) purchased, the shopper's addresses, the payment method used for the order, and more. To learn about creating orders, see [Orders Overview](https://developer.bigcommerce.com/api-docs/orders/orders-overview).

## V2 & V3
Order resources use either the V2 or V3 REST APIs. See the corresponding reference for each resource to determine the correct path.

## Order Products
v2
Product line items belonging to an order.

## Order Status
v2
Each order status represents a state in the order-fulfillment workflow.

## Order Shipping Addresses
v2
Customer shipping address belonging to an order.

## Order Shipping Addresses Quotes
v2
Read Only. Get’s all shipping quotes from an order.


## Order Taxes
v2
Tax will be calculated based on the tax rules specified in the store, except in the case of automatic taxes. However, in both cases, you can optionally override the tax values by specifying `price_inc_tax` and `price_ex_tax`.

### Avalara

Merchants have the option to enable automatic tax calculation for orders with [Avalara](https://support.bigcommerce.com/s/article/Avalara-Avatax-Sales-Tax-Calculation).

When the store is subscribed to Avalara Premium, a value of API Tax Override is written to the Order Tax object’s name field.

Abbreviated state names in shipping and billing addresses will prevent tax documents from being submitted to Avalara. To ensure successful Avalara tax-document submission, spell state names out in full. For example, supplying CA as a state name leads to no tax-document submission. Supplying California as a state name leads to a successful submission.

POST or PUT orders on stores with Avalara Premium cause tax documents to be submitted. If a store has subscribed to Avalara Premium, BigCommerce automatically submits tax documents to Avalara when the order achieves a paid status. See Order Status below for a list of paid statuses.

You can create overrides for calculated values such as product prices, subtotal and totals by sending a fixed value in the request. If values are not supplied for these properties, they will be automatically calculated based on the preset store values and tax rules.

| Existing Status | Status Passed | Resultant Status | Avalara Tax Document Submission |
| - | - | - | - |
| Any | None | `Pending` | None |
| Paid or `Refunded` | Paid | Paid | None |
| Unpaid or `Refunded` | Unpaid | Unpaid | None |
| Paid or `Refunded` | Unpaid | Unpaid | Tax document voided |
| Unpaid or `Refunded` | Paid | Paid | Tax document submitted |

## Order Coupons
v2
Coupon code applied to an order.

## Order Shipments
We will go over creating a shipment for an order, shipping quotes, shipping carriers and shipping to multiple locations.

### Create an Order Shipment

**Required Fields:**
* order_address_id
* shipping_provider
* items

Once an Order has products, a billing address and at least one shipping address a order shipment can be created. Order shipments are a way to mark an order as shipped with the shipping information.

To get the `order_address_id`  use the ID returned in [Order Shipping Address](https://developer.bigcommerce.com/api-reference/orders/orders-api/order-shipping-addresses/getallshippingaddresses).

The items array requires the product quantity and `order_product_id`. The `order_product_id` is the ID returned from [Order Products](https://developer.bigcommerce.com/api-reference/orders/orders-api/order-products/getanorderproduct).

There does not need to be a shipping provider. If the shipping provider is not sent in at all, it will default to custom and a tracking link is not generated. To have the tracking link generated without a shipping provider, provide an empty string. To add a shipping provider, see the available options on [Order Shipment](https://developer.bigcommerce.com/api-reference/orders/orders-api/order-shipments/getallordershipments).

Once the order shipment is created, it will automatically send out an email to the billing address with the shipment confirmation. To stop this behavior adjust the [Order Notification](https://support.bigcommerce.com/s/article/Customer-Order-Notifications#enable) settings in the Control Panel.

If the order shipment is deleted, the status of the shipment is still in shipped. The status will need to be [manually changed](https://developer.bigcommerce.com/api-reference/orders/orders-api/order-status/getaorderstatus).

<br>

<!--
title: "Create Order Shipment"
subtitle: ""
lineNumbers: true
-->

**Example Create Order Shipment**
`https://api.bigcommerce.com/stores/{store_hash}/v2/orders/{order_id}/shipments`

```json
{
  "tracking_number": "EJ958083578UK",
  "comments": "Janes Order",
  "order_address_id": "128",
  "shipping_provider": "",
  "items": [
        {
            "order_product_id": 194,
            "product_id": 0,
            "quantity": 1
        },
        {
            "order_product_id": 195,
            "product_id": 0,
            "quantity": 1
        }
  ]
}
```

<!--
title: "Order Shipment Response"
subtitle: ""
lineNumbers: true
-->

**Example Order Shipment Response**

```json
{
    "id": 11,
    "order_id": 228,
    "customer_id": 11,
    "order_address_id": 131,
    "date_created": "Wed, 13 Mar 2019 16:35:37 +0000",
    "tracking_number": "EJ958083578US",
    "merchant_shipping_cost": "0.0000",
    "shipping_method": "None",
    "comments": "Ready to go...",
    "shipping_provider": "",
    "tracking_carrier": "",
    "billing_address": {
        "first_name": "Jane",
        "last_name": "Doe",
        "company": "",
        "street_1": "123 Main Street",
        "street_2": "",
        "city": "Austin",
        "state": "Texas",
        "zip": "78751",
        "country": "United States",
        "country_iso2": "US",
        "phone": "",
        "email": "janedoe@email.com"
    },
    "shipping_address": {
        "first_name": "Trishy",
        "last_name": "Test",
        "company": "Acme Pty Ltd",
        "street_1": "666 Sussex St",
        "street_2": "",
        "city": "Anywhere",
        "state": "Some State",
        "zip": "12345",
        "country": "United States",
        "country_iso2": "US",
        "phone": "",
        "email": "elsie@example.com"
    },
    "items": [
        {
            "order_product_id": 194,
            "product_id": 0,
            "quantity": 1
        },
        {
            "order_product_id": 195,
            "product_id": 0,
            "quantity": 1
        }
    ]
}

```

### Multiple Locations

Orders can have multiple shipment locations. There needs to be more than one product or quantity of a product and more than one shipping addresses. A shipping address can be added either during the create or using an update.

To ship to multiple locations create an order shipment for each location and items. Only one POST request per shipment.

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

<!-- theme:  -->
### Shipping Address
> When adding shipping addresses during an order PUT or POST, the API will allow you to add more than is necessary.

</div>
</div>
</div>

### Custom Quotes
An order can be created with a `shipping_cost_ex_tax` and `shipping_cost_inc_tax`. This is a way to add a custom shipping amount to an order. This can be added when creating or updating an order.

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

<!-- theme:  -->
### Shipping Cost
> Both `shipping_cost_ex_tax` and `shipping_cost_inc_tax` must be included otherwise, the final order amount will not be calculated correctly.

</div>
</div>
</div>

### Shipping Carrier
Generating a quote through a shipping carrier is currently not supported. A shipping carrier can be specified when creating an Order Shipment. The quote can be generate elsewhere, then update the `shipping_cost_ex_tax` and `shipping_cost_inc_tax` for the order total to be correct..


If a store has automatic tax enabled, BigCommerce does not compute sales tax on orders created via the API.


## Order Messages
v2
Messages associated with an order.

## Order Currency Fields

* `currency_code` - the display currency used to present prices to the shopper on the storefront.
* `currency_exchange_rate`: the exchange rate between the store's default currency and the display currency; when the order is created by means of the V2 endpoints, this value is always 1 (only in the storefront this value can be different to 1).

The following additional fields are returned on orders when Multi-Currency is enabled on the store:

* `store_default_currency_code` - the store's default currency
* `store_default_to_transactional_exchange_rate` - the exchange rate between the store's default currency and the transactional currency used in the order.

**Example:**

```json
{
  ...
  "currency_id": 4,
  "currency_code": "EUR",
  "currency_exchange_rate": 1,
  "default_currency_id": 4,
  "default_currency_code": "EUR",
  "store_default_currency_codev": "USD",
  "store_default_to_transactional_exchange_rate": "100.0000000000"
  ...
}

```



## Order Transactions
v3
The `/orders/{id}/transactions` endpoint returns details about the payment instruments used to pay for an order. Depending on the payment method used, different details will be available. Not all credit card payment gateways will return full card details or all CVV/fraud response details. This is primarily used to get detailed gateway response information for credit card transactions, however it will also return any available information about digital wallet payments, as well as details about orders paid (partially or in full) via a gift certificate or store credit. The test payment gateway available in the BigCommerce control panel does not return any payment information.

Orders processed via all payment providers except PayPal Express Checkout and Test Gateway will create a transaction that is retrievable via Transactions API. Gift certificates, store credit, and offline payment methods will not create a transaction.

## Order Payment Actions
v3
### Refunds

## Order Returns
v3
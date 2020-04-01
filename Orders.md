# Orders

<div class="otp" id="no-index">

### On this Page	
- [Orders](#orders)
- [Order Currency Fields](#order-currency-fields)
- [Order Coupons](#order-coupons)
- [Order Messages](#order-messages)
- [Order Products](#order-products)
- [Order Status](#order-status)
- [Order Shipments](#order-shipments)
- [Order Shipping Addresses](#order-shipping-addresses)
- [Order Shipping Addresses Quotes](#order-shipping-addresses-quotes)
- [Order Taxes](#order-taxes)
- [Order Transactions](#order-transactions)


</div>

## Orders
The Order object contains a record of the purchase agreement between a shopper and a merchant. To learn more about creating orders, see [Orders Overview](https://developer.bigcommerce.com/api-docs/orders/orders-overview).

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

## Order Coupons
v2
Coupon code applied to an order.

## Order Messages
v2
Messages associated with an order.

## Order Products
v2
Product line items belonging to an order.

## Order Status
v2
Each order status represents a state in the order-fulfillment workflow.

## Order Shipments
v2
Tracks a package consignment from an order that is shipped from the seller to the buyer.

## Order Shipping Addresses
v2
Customer shipping address belonging to an order.

## Order Shipping Addresses Quotes
v2
Read Only. Get’s all shipping quotes from an order.

## Order Taxes
v2
Each tax applied to an order. This information can be useful for reporting purposes. All values are read-only.

## Order Transactions
v3
The `/orders/{id}/transactions` endpoint returns details about the payment instruments used to pay for an order. Depending on the payment method used, different details will be available. Not all credit card payment gateways will return full card details or all CVV/fraud response details. This is primarily used to get detailed gateway response information for credit card transactions, however it will also return any available information about digital wallet payments, as well as details about orders paid (partially or in full) via a gift certificate or store credit. The test payment gateway available in the BigCommerce control panel does not return any payment information.

Orders processed via all payment providers except PayPal Express Checkout and Test Gateway will create a transaction that is retrievable via Transactions API. Gift certificates, store credit, and offline payment methods will not create a transaction.
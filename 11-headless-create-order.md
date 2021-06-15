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

[Create a Cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart) with a redirect url by including the `include=redirect_urls` query parameter.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/carts?include=redirect_urls
X-Auth-Token: {{ACCESS_TOKEN}}

{
  "custom_items": [
    {
      "sku": "abc-123",
      "name": "Custom Product",
      "quantity": 1,
      "list_price": 10
    }
  ]
}
```

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart#requestrunner)

**Response:**

```json
{
  "data": {
    "base_amount": 10,
    "cart_amount": 10.83,
    "channel_id": 1,
    ...
    "id": "bceae094-36de-418e-b3d5-979bdb706842",
    ...
    "redirect_urls": {
      "cart_url": "https://store.example.com/cart.php?action=load&id=bceae094-...",
      "checkout_url": "https://store.example.com/cart.php?action=loadInCheckout&id=bceae094-...",
      "embedded_checkout_url": "https://store.example.com/cart.php?embedded=1&action=loadInCheckout&id=bceae094-..."
    },
    "tax_included": false,
    "updated_time": "2021-06-15T19:06:22+00:00"
  },
  "meta": {}
}
```


<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

> ### Note
> * Add the Customer ID or leave blank if shopper is a guest.
> * Add Line Items or Custom Line Items.

</div>
</div>
</div>


## Add a billing address

Add a [Billing Address](/api-reference/cart-checkout/server-server-checkout-api/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost) to the [Cart](/api-reference/cart-checkout/server-server-cart-api/cart/createacart) changing it to a Checkout. To [add checkout billing address](https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost), send a `POST` request to `/stores/{{STORE_HASH}}/v3/checkouts/{checkoutId}/billing-address`.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/checkouts/{checkoutId}/billing-address
X-Auth-Token: {{ACCESS_TOKEN}}

{
  "first_name": "Jane",
  "last_name": "Doe",
  "email": "jane@example.com",
  "address1": "123 Main Street",
  "address2": "",
  "city": "Austin",
  "state_or_province": "Texas",
  "state_or_province_code": "TX",
  "country_code": "US",
  "postal_code": "78751",
  "phone": "1234567890"
}
```

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-billing-address/checkoutsbillingaddressbycheckoutidpost#requestrunner)

## Add a consignment

Add a [Consignment](/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments/checkoutsconsignmentsbycheckoutidpost) to Checkout with the line items and the `consignments.available_shipping_options` query. To [add a consignment to a checkout](https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-consignments/checkoutsconsignmentsbycheckoutidpost), send a `POST` request to `/stores/{{STORE_HASH}}/v3/checkouts/{checkoutId}/consignments`.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/checkouts/{checkoutId}/consignments
X-Auth-Token: {{ACCESS_TOKEN}}

[
  {
    "shipping_address": {
      "email": "jane2@example.com",
      "country_code": "US",
      "first_name": "BigCommerce",
      "last_name": "Cart/Checkout",
      "address1": "123 Main Street",
      "city": "Austin",
      "state_or_province": "Texas",
      "state_or_province_code": "TX",
      "postal_code": "78751",
      "phone": "688546",
      "custom_fields": [
        {
          "field_id": "field_25",
          "field_value": "Great!"
        }
      ]
    },
    "line_items": [
      {
        "item_id": "{{LINE_ITEM_ID}}",
        "quantity": 1
      }
    ]
  }
]
```

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-consignments/checkoutsconsignmentsbycheckoutidpost#requestrunner)

## Update consignment with shipping options

https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-consignments/checkoutsconsignmentsbycheckoutidandconsignmentidput

Update each [Consignment](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api/checkout-consignments) with the chosen shipping option from the Add Consignment response.

## Create the order

https://developer.bigcommerce.com/api-reference/store-management/checkouts/checkout-orders/createanorder

Create the Order by sending a request to [Create Order](/api-reference/cart-checkout/server-server-checkout-api/checkout/createanorder)
* Returns an `order_id`
* Order is created in `incomplete` status

## Resources

* [Carts API](https://developer.bigcommerce.com/api-reference/storefront/carts)
* [Checkouts API](https://developer.bigcommerce.com/api-reference/store-management/checkouts)
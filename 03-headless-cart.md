# Creating Carts

<div class="otp" id="no-index">

### On this Page	
- [Resources](#resources)

</div>

This section demonstrates how to use the [Server to Server Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts) to generate an active cart and manage abandoned carts.

## Creating carts

The [Server to Server Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts) allows you to create carts for both existing and guest customers. To create an active cart, send a `POST` request to `/v3/carts`.

```http
POST https://api.bigcommerce.com/stores/{store_hash}/v3/carts
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

**Create a Cart request example**

```json
{
  "channel_id": 20266,
  "line_items": [
    {
      "quantity": 1,
      "product_id": 80,
      "variant_id": 64
    }
  ]
}
```

To create a cart for an existing customer, include the `customer_id` in your `POST` request.

```json
{
  "customer_id": 42,
  "line_items": [
    {
      "quantity": 5,
      "product_id": 191
    }
  ]
}
```

The `id` returned in the response corresponds to the `cart_id` required to generate cart redirect URLs.

### Guest cart

A guest cart assumes the shopper is not a customer and is not logging in or creating an account during checkout. You can handle guest checkouts by displaying the cart data to the customer and then moving them to Checkout using the [Checkouts API](https://developer.bigcommerce.com/api-reference/store-management/checkouts).

## Redirecting to checkout

When creating a cart, there is an optional query to create a redirect URL. Use this to redirect the shopper to a BigCommerce hosted checkout page.

## Clearing the cart

Content

## Abandoned carts

The [Abandoned Carts API](https://developer.bigcommerce.com/api-reference/store-management/abandoned-carts) makes it possible to retrieve the `cart_id` of the abandoned cart. The `cart_id` will correspond to the token in the query string of the link included in abandoned cart notification emails. 

To do so, follow these steps:

1. Because the `cart_id` corresponds to the abandoned cart token found in the query string of the link included in abandoned cart notification emails, you need to provide this token to retrieve the `cart_id`.
2. Pass the abandoned cart token in a `GET` request to `/v3/abandoned-carts/{token}`. 

Once you retrieve the `cart_id`, you can use it to fetch and display information about the cart to the shopper via the [Storefront Carts](https://developer.bigcommerce.com/api-reference/storefront/carts) and [Server to Server Carts](https://developer.bigcommerce.com/api-reference/store-management/carts) APIs.

## Next Steps
* [Learn how to move the cart to checkout]().

## Resources
* [Server to Server Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts)
* [Storefront Carts](https://developer.bigcommerce.com/api-reference/storefront/carts)
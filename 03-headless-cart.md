# Creating Carts

<div class="otp" id="no-index">

### On this page
- [Creating carts](#creating-carts)
- [Redirecting to checkout](#redirecting-to-checkout)
- [Clearing the cart](#clearing-the-cart)
- [Abandoned carts](#abandoned-carts)
- [Resources](#resources)

</div>

This section demonstrates how to use the [Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts) to generate an active cart, redirect shoppers to checkout, and manage abandoned carts.

## Creating carts

The [Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts) allows you to create carts for both existing and guest customers. To create an active cart, send a `POST` request to the [Create a Cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart) endpoint.

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

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

> ### Note
> The `id` returned in the response corresponds to the `cart_id` required to generate cart redirect URLs.

</div>
</div>
</div>

### Guest cart

A guest cart assumes the shopper is not a customer and is not logging in or creating an account during checkout. You can handle guest carts by displaying the cart data to the customer and then moving them to checkout using the [Checkouts API](https://developer.bigcommerce.com/api-reference/store-management/checkouts).

## Redirecting to checkout

A cart redirect URL redirects a shopper to a BigCommerce hosted checkout page. Redirect URLs can be generated **only** from carts created using the Carts API.

To generate a cart redirect URL, send a `POST` request to the [Create Cart Redirect URL](https://developer.bigcommerce.com/api-reference/store-management/carts/cart-redirect-urls/createcartredirecturl) endpoint. The `cartId` path parameter corresponds to the `id` returned in the [Create a Cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart) response.

```http
POST https://api.bigcommerce.com/stores/{store_hash}/v3/carts/{cartId}/redirect_urls
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

### Creating a redirect using the include query parameter

It is possible to generate a redirect URL when creating a cart using the [Create a Cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart) endpoint by appending the `include=redirect_urls` query parameter to the request URL.

## Clearing the cart

Removing all cart items essentially deletes the cart. To clear the cart, call the Carts API [Delete a Cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/deleteacart) endpoint.

```http
DELETE https://api.bigcommerce.com/stores/{store_hash}/v3/carts/{cartId}
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

To delete a line item from a cart, send a `DELETE` request to the [Delete Cart Line Item](https://developer.bigcommerce.com/api-reference/store-management/carts/cart-items/deletecartlineitem) endpoint and pass in the associated `cartId` and `itemId`. 

```http
DELETE https://api.bigcommerce.com/stores/{store_hash}/v3/carts/{cartId}/items/{itemId}
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

## Abandoned carts

The [Abandoned Carts API](https://developer.bigcommerce.com/api-reference/store-management/abandoned-carts) makes it possible to retrieve the `cart_id` of the abandoned cart which can then be used to fetch and display information about the cart to the shopper. The `cart_id` corresponds to the token in the query string of the abandoned cart link provided in abandoned cart email notifications. 

To retrieve the `cart_id`, follow these steps:

1. By default, customers receive abandoned cart emails as soon as they provide their email address in the checkout flow. Those notification emails contain a link to the cart abandoned by the shopper. You need to retrieve the abandoned cart token found in the query string of the abandoned cart link.

2. Pass the abandoned cart token in a `GET` request to the [Get an Abandoned Cart](https://developer.bigcommerce.com/api-reference/store-management/abandoned-carts/abandoned-carts/getabandonedcarts) endpoint to retrieve the `cart_id`. 

3. Once you retrieve the `cart_id`, you can use it to request information about the cart and display it to the shopper using the [Storefront Carts](https://developer.bigcommerce.com/api-reference/storefront/carts) and [Carts](https://developer.bigcommerce.com/api-reference/store-management/carts) APIs.

## Next Steps
* [Learn how to move the cart to checkout]().

## Resources
* [Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts)
* [Storefront Carts](https://developer.bigcommerce.com/api-reference/storefront/carts)
* [Persistent Cart](https://support.bigcommerce.com/s/article/Persistent-Cart)
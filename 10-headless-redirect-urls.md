# Generating Redirect URLs

<div class="otp" id="no-index">

### On this Page
- [Create a cart](#create-a-cart)
- [Generate redirect URLs](#generate-redirect-urls)
- [Resources](#resources)

</div>

This tutorial explains how to use the [Cart API](https://developer.bigcommerce.com/api-reference/store-management/carts) to generate a cart and checkout redirect URLs that can be used to redirect from a headless storefront to the BigCommerce hosted cart and checkout pages, or used with the Checkout SDK to embed the BigCommerce hosted checkout into the headless site.

## Create a cart

We'll need the `id` of an active cart to generate the redirect URLs. To [create a cart](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart), send a `POST` request to `/stores/{{STORE_HASH}}/v3/carts`.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/carts
X-Auth-Token: {{ACCESS_TOKEN}}

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

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/carts/cart/createacart#requestrunner)

If you are creating a cart for a specific customer, pass in the `customer_id` in the request.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/carts
X-Auth-Token: {{ACCESS_TOKEN}}

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

Contained in the response is an `id`, which we'll use as the `cart_id` in the next request.

```json
{
    "data": {
        "id": "33608b81-ba34-4ff2-8bab-2771aeab3f73",
    ...
}
```

## Generate redirect URLs

Next, use the `id` from the create cart response to generate the the redirect URLs. To do so, send a `POST` request to `/stores/{{STORE_HASH}}/v3/carts/{{CART_ID}}/redirect_urls`.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/carts/{{CART_ID}}/redirect_urls
X-Auth-Token: {{ACCESS_TOKEN}}
```

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/carts/cart-redirect-urls/createcartredirecturl#requestrunner)

The response contains redirect URLs for cart and checkout (`cart_url` and `checkout_url`) -- use these URLs to redirect the customer to the BigCommerce hosted cart or checkout page. The `embedded_checkout_url` can be used with the Checkout SDK to embed the BigCommerce hosted checkout into a headless site via iFrame.

```json
{
  "cart_url": "https://store-id30h7ohwf.mybigcommerce.com/cart.php?action=load&id=bc218c65-7a32-4ab7-8082-68730c074d02&token=aa958e2b7922035bf3339215d95d145ebd9193deb36ae847caa780aa2e003e4b",
  "checkout_url": "https://store-id30h7ohwf.mybigcommerce.com/cart.php?action=loadInCheckout&id=bc218c65-7a32-4ab7-8082-68730c074d02&token=aa958e2b7922035bf3339215d95d145ebd9193deb36ae847caa780aa2e003e4b",
  "embedded_checkout_url": "https://store-id30h7ohwf.mybigcommerce.com/cart.php?embedded=1&action=loadInCheckout&id=bc218c65-7a32-4ab7-8082-68730c074d02&token=aa958e2b7922035bf3339215d95d145ebd9193deb36ae847caa780aa2e003e4b"
}
```

## Login and redirect a customer

If you passed in a `customer_id` in the create cart request, you'll need to tell BigCommerce to login the customer before redirecting to the cart or checkout. To do so, create a customer login `JWT` using the same `customer_id`, and set the `redirect_to` parameter to the relative path of the desired redirect URL. Below is an example customer login `JWT` payload.


```json
{
  "iss": {{CLIENT_ID}},
  "iat": 1535393113,
  "jti": {{UUID}},
  "operation": "customer_login",
  "store_hash": {{STORE_HASH}},
  "customer_id": {{CUSTOMER_ID}},
  "channel_id": {{CHANNEL_ID}},
  "redirect_to": "/cart.php?embedded=1&action=loadInCheckout&id=bc218c65-7a32-4ab7-8082-68730c074d02&token=aa958e2b7922035bf3339215d95d145ebd9193deb36ae847caa780aa2e003e4b",
  "request_ip": "111.222.333.444"
}
```

Use the payload to generate the customer login `JWT`. Then, create a customer login URL by appending the `JWT` to `https://{{YOUR_BIGCOMMERCE_DOMAIN}}.com/login/token/`. Below is an example.

```
https://store.example.com/login/token/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ7Y2xpZW50X2lkfSIsImlhdCI6MTUzNTM5MzExMywianRpIjoie3V1aWR9Iiwib3BlcmF0aW9uIjoiY3VzdG9tZXJfbG9naW4iLCJzdG9yZV9oYXNoIjoie3N0b3JlX2hhc2h9IiwiY3VzdG9tZXJfaWQiOjJ9.J-fAtbjRFGdLsT744DhoprFEDqIfVq72HbDzrbFy6Is
```

Redirect the customer to the login URL to log them in before redirecting to the cart or checkout. If you're using Embedded Checkout, pass the customer login URL to the Checkout SDK to login the customer, then redirect to checkout within the embedded checkout iFrame. 

This customer login JWT must also include a `channel_id` property, which is currently undocumented. If this channel ID is not included, CORS checks will fail and the checkout won't load.

## Resources

* [Carts API](https://developer.bigcommerce.com/api-reference/store-management/carts)
* [Checkouts API](https://developer.bigcommerce.com/api-reference/store-management/checkouts)
* [Customer Login API](https://developer.bigcommerce.com/api-docs/storefront/customer-login-api)
* [Embedded Checkout Tutorial](https://developer.bigcommerce.com/api-docs/storefronts/embedded-checkout/embedded-checkout-tutorial)
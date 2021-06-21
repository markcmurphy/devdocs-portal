# Managing Customers

<div class="otp" id="no-index">

### On this Page

- [Client-side GraphQL customer login](#client-side-graphql-customer-login)
- [Server-side GraphQL customer login](#server-side-graphql-customer-login)
- [Surfacing customer group pricing](#surfacing-customer-group-pricing)
- [Customer Single Sign-on](#customer-single-sign-on)
- [Identifying logged-in customers](#identifying-logged-in-customers)
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

Introduction

## Client-side GraphQL customer login

In client-side code, use the [Storefront GraphQL API](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview) customer login mutation to log in a customer account with an email address and a password.

```js
mutation Login($email: String!, $pass: String!) {
  login(email: $email, password: $pass) {
    result
  }
}
```

When a customer is logged in using the customer login mutation, subsequent quereies made to the Storefront GraphQL API return customer-specific results (like customer group pricing, for example) using the context of the logged in customer.

[Learn more about using the Storefront GraphQL API to login customers](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-login).

## Server-side GraphQL customer login

To make queries from the perspective of a particular customer in server-side code, use customer impersonation tokens.

Customer impersonation token authenticated requests made to the GraphQL API receive store information from the perspective of the customer corresponding to the customer ID specified in the `X-Bc-Customer-Id` header sent with the GraphQL `POST` request. **Pricing**, **product availability**, **customer account**, and **customer details** will be reflected.

[Learn more about GraphQL Storefront API customer impersonation tokens](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-impersonation-tokens).

## Surfacing customer group pricing

When querying the GraphQL storefront API, customer-specific pricing will be reflected in query results if the customer is first logged-in using the [customer login mutation](#client-side-graphql-customer-login) or a [customer impersonation token](#server-side-graphql-customer-login).

For server-side REST implimentations, use the [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing) to [get prices](https://developer.bigcommerce.com/api-reference/store-management/pricing/products/get-prices) for a particular customer group.

```http
POST https://api.bigcommerce.com/stores/{{STORE_HASH}}/v3/pricing/products
X-Auth-Token: {{ACCESS_TOKEN}}

{
  "channel_id": 1,
  "currency_code": "USD",
  "customer_group_id": 0,
  "items": [
    {
      "product_id": 0,
      "variant_id": 0,
      "options": [
        {
          "option_id": 0,
          "value_id": 0
        }
      ]
    }
  ]
}
```

[![Open in Request Runner](https://storage.googleapis.com/bigcommerce-production-dev-center/images/Open-Request-Runner.svg)](https://developer.bigcommerce.com/api-reference/store-management/pricing/products/get-prices#requestrunner)

**Response:**

```json
{
  "data": [
    {
      "product_id": 1,
      "variant_id": 1,
      "options": [...],
      "retail_price": {
        "as_entered": 1.5,
        "entered_inclusive": true,
        "tax_exclusive": 1.1,
        "tax_inclusive": 1.5
      },
      "sale_price": {...},
      "minimum_advertised_price": {...},
      "price": {...},
      "calculated_price": {...},
      "price_range": {...},
      "retail_price_range": {...},
      "bulk_pricing": [...]
    }
  ],
  "meta": {}
}
```

[Learn more about the Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing).

## Customer Single Sign-on

If a customer logs in to your headless storefront, and then is redirected to a BigCommerce-hosted page, you can use the Customer Login API to create a single sign-on experience between your headless storefront and BigCommerce. Doing so will make the redirection from the headless storefront to BigCommerce a more seemless experience for the customer.

[Learn more about using the Customer Login API to create a single sign-on experience](https://developer.bigcommerce.com/api-docs/storefront/current-customer-api).

You can seemlessly login a customer into an embedded checkout by setting `redirect_to` in the Customer Login JWT payload to the relative path of the `embedded_checkout_url` generated using the Carts API.

```
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

[Learn more about generating cart and checkout redirect URLs](%2Fapi-docs%2Fstorefronts%2Ftutorials%2Fredirect-urls).

## Identifying logged-in customers

If a customer logs in to a BigCommerce-hosted cart or checkout, then navigates back to the headless storefront, you'll need to confirm the customer's identity before revealing sensitive information.

To address this need, BigCommerce provides a [Current Customer API](https://developer.bigcommerce.com/api-docs/storefront/current-customer-api) which can be accessed via client-side JavaScript. This endpoint returns a `JWT` (signed with your OAuth client secret) that contains customer details.

[Learn how to use the Current Customer API to identify logged-in customers securely](https://developer.bigcommerce.com/api-docs/storefront/current-customer-api).



## Next Steps

* [Learn how to create orders](/api-docs/storefronts/guide/orders).

## Resources

* [Customer Login API](https://developer.bigcommerce.com/api-docs/storefront/customer-login-api)
* [GraphQL Storefront API Customer Impersonation Tokens](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-impersonation-tokens)
* [GraphQL Storefront API Custom Login Mutation](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-login)
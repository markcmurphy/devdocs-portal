# Managing Customers

<div class="otp" id="no-index">

### On this Page

- [Logging in customers](#logging-in-customers)
- [Surfacing customer group pricing](#surfacing-customer-group-pricing)
- [Associating customers with carts](#associating-customers-with-carts)
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

In this article, we'll discuss how to manage customer interactions on headless storefronts.

## Logging in customers

{{Briefly discuss the different options, then link to relavent tutorials / docs}}

### GraphQL customer login mutation

{{For making graphql queries from a customer's perspective in the browser}}

If you're logging the customer in from a browser, you can use the Storefront GraphQL API customer login mutation to log in a customer account with an email address and a password.

```js
mutation Login($email: String!, $pass: String!) {
  login(email: $email, password: $pass) {
    result
  }
}
```

[Learn more about using the Storefront GraphQL API to login customers](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-login)

### GraphQL customer impersonation tokens

{{For making graphql queries from a customer's perspective (server-side only)}}

For server-side integrations, consider a customer impersonation token instead. This will set a session cookie in the browser which will authenticate the customer account on future requests.

Customer impersonation token authenticated requests made to the GraphQL API receive store information from the perspective of the customer corresponding to the customer ID specified in the `X-Bc-Customer-Id` header sent with the GraphQL `POST` request. **Pricing**, **product availability**, **customer account**, and **customer details** will be reflected.

[Learn more about GraphQL Storefront API customer impersonation tokens](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-impersonation-tokens).

### Customer Login API

{{Briefly explain that the customer login api is for creating BigCommerce URLs that log the customer in to the BigCommerce storefront automatically (so they don't have to login to the headless storefront, then login again to the BC storefront when redirected to cart or checkout); then, link to the Customer Login API tutorial}}

## Surfacing customer group pricing

{{If the customer is logged in or a customer impersonation token is being used, customer group pricing will be reflected; is there a non-graphql way? Pricing API maybe?}}

## Associating customers with carts

{{I think this is pretty much covered in the generating redirect URLs tutorial, but may be worth summarizing here or splitting into a separate tutorial. Need to do more research.}}

## Next Steps

* [Learn how to create orders]().

## Resources

* [Customer Login API](https://developer.bigcommerce.com/api-docs/storefront/customer-login-api)
* [GraphQL Storefront API Customer Impersonation Tokens](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-impersonation-tokens)
* [GraphQL Storefront API Custom Login Mutation](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-login)
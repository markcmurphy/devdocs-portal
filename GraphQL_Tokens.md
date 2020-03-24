# GraphQL Tokens

<div class="otp" id="no-index">

### On this Page	
- [GraphQL Tokens](#graphql-tokens)
- [API Tokens](#api-tokens)
- [Customer Impersonation Token](#customer-impersonation-token)
</div>

GraphQL Storefront API requests are authenticated with tokens sent via the HTTP Authorization header

## GraphQL Tokens

## API Tokens

## Customer Impersonation Token
Its also possible to generate tokens for use in server-to-server interactions with a trusted consumer by POSTing to the [API Token Customer Impersonation Endpoint](https://developer.bigcommerce.com/api-reference/storefront/graphql-api-tokens/api-token-customer-impersonation/createtokenwithcustomerimpersonation) with the `X-Bc-Customer-Id` header set to the customer's ID:

**`POST`** `https://api.bigcommerce.com/stores/{store_id}/v3/storefront/api-token-customer-impersonation`

```json
{
  "channel_id": 1,
  "expires_at": 1602288000
}
```

**Response**:

```json
{
  "data":
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
  }
  "meta": {}
}
```

Customer Impersonation Token authenticated requests made to the GraphQL API receive store information from the perspective of the customer corresponding to the customer ID specified in the `X-Bc-Customer-Id` header used to create the token -- for example: pricing, product availability, customer account, and customer details.
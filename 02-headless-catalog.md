# Catalog

<div class="otp" id="no-index">

### On this Page
- [Create a channel](#create-a-channel)
- [Render pages](#render-pages)
- [Manage product data](#manage-product-data)
- [Best practices](#best-practices)
- [Next steps](#next-steps)
- [Resources](#resources)

</div>
</br>


This section demonstrates how to use BigCommerce's GraphQL Storefront API to query product data for headless storefronts. 

## Create a channel

Before you can display products on a headless storefront, you need to create a channel and a channel site for that storefront. A channel is essentially a sales platform such as a headless storefront, a marketplace, or a POS system. A site is a domain that links a headless storefront to a sales channel.

You can create both using the [Channels API](https://developer.bigcommerce.com/api-reference/store-management/channels). 

Start by sending a `POST` request to the `/channels` endpoint to create a channel for your headless platform. Retrieve the channel ID returned in the response. You will use it to create a channel site and authenticate cross-origin requests. 

Next, pass that channel ID in a `POST` request to `/channels/{channel_id}/site` to create a site for the provided channel. 

Now that you have set up your channel, you can authenticate cross-origin requests by [creating a JWT token](https://developer.bigcommerce.com/api-reference/storefront/graphql#tokens-via-api) through the Storefront API. Make sure to create your Storefront API token with the same channel ID as your headless platform; otherwise, your request will be rejected.

## Render pages

BigCommerce’s GraphQL Storefront API makes it possible to query storefront data from a remote site. By leveraging the power of GraphQL, you can access product information for any product from any page.

The following example demonstrates how to fetch product data using the GraphQL Storefront API. It follows the [GraphQL Cursor Connections Specification](https://relay.dev/graphql/connections.htm) model and shows a simple GraphQL query for a store's products.

**Product Listing page query example**

```js
function getProductInfo(params) {
    const storeUrl = new URL(params.store_url);

    // Use the store's canonical URL which should always resolve
    const graphQLUrl = `${storeUrl.origin}/graphql`;

    // Set up GraphQL query
    const graphQLQuery = `
        query productListing {
            site {
                products {
                    pageInfo {
                        startCursor
                        endCursor
                        }
                    edges {
                        cursor
                        node {
                            id
                            entityId
                            name
                            sku
                            description
                            prices {
                                price {
                                    value
                                    currencyCode
                                }
                            }
                        }
                    }
                }
            }
        }`

    // Fetch data from the GraphQL Storefront API
    return fetch(graphQLUrl, {
        method: 'POST',
        credentials: 'include',
        mode: 'cors',
        headers: { 
            'Content-Type': 'application/json', 
            'Authorization': `Bearer ${params.token}`},
            body: JSON.stringify({ query: graphQLQuery}),
        })
        .then(res => res.json())
        .then(res => res.data);
    }

    // Set up default params
    let params = {
        store_url: null,
        token: null
    };
```

Following the same API fetching logic, you can retrieve single product data. The following example shows a GraphQL Storefront API query for a single product.

**Product Details page query example**

```
query SingleProduct {
  site {
    products (entityIds: ${props.id}) {
      id
      entityId
      name
      sku
      description
      prices {
        price {
          value
          currencyCode
        }
      }
    }
  }
}
```
## Manage product data

BigCommerce's [Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api) enables you to manage catalog data. To retrieve the complete list of products, send a `GET` request to `/v3/catalog/products`. You can pass optional query string parameters to influence the response. We recommend caching the product data and storing it in a database to improve performance.

```http
GET https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

Using the [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing), you can control the pricing displayed for a particular channel or a customer group on your storefront.

**Override pricing using the Pricing API**

The [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing) lets you override product pricing for a specific channel or customer group. To override the price for each of the sellable items on the page, supply their product IDs (required) and variant IDs (optional) in a `POST` request to `/v3/pricing/products`.

The following example shows how use the Pricing API to assign customer group pricing.

```http
POST https://api.bigcommerce.com/stores/{store_hash}/v3/pricing/products
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}

{
  "channel_id": 1,
  "currency_code": "USD",
  "customer_group_id": 1,
  "items": [
    {"product_id": 77},
    {"product_id": 80},
    {"product_id": 81},
    {"product_id": 86}
  ]
}
```

## Best Practices

**Cache the catalog**

It is best practice to cache product details in a database to improve data retrieval and increase operational efficiency. Caching product information will allow you to implement search functionality and enable you to control the information displayed to the customers. 

**Return real-time product data**

You can use the Catalog API to retrieve real-time catalog data. 

**Return real-time pricing and inventory data**

If you prefer working with a local copy of your catalog, but want to make sure that high priority pieces of data like pricing and inventory stay current, consider a hybrid model. With a hybrid model, you cache only certain product details and pull the other information in real time.

## Next Steps
* [Learn how to create carts headlessly]().

## Resources
* [Catalog API Overview](https://developer.bigcommerce.com/api-docs/store-management/catalog/catalog-overview)
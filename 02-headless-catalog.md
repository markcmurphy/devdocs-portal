# Catalog

<div class="otp" id="no-index">

### On this Page
- [Rendering pages](#rendering-pages)
- [Managing product data](#managing-product-data)
- [Using the Pricing API](#using-the-pricing-api)
- [Best practices](#best-practices)
- [Next steps](#next-steps)
- [Resources](#resources)

</div>
</br>


This section demonstrates how to use BigCommerce's GraphQL Storefront API to query product data for headless storefronts. 

## Rendering pages

BigCommerce’s [GraphQL Storefront API](https://developer.bigcommerce.com/api-reference/storefront/graphql) makes it possible to query storefront data from a remote site. By leveraging the power of GraphQL, you can access product information for any product from any page.

The following example demonstrates how to fetch product data using the GraphQL Storefront API. It relies on the [GraphQL Cursor Connections Specification](https://relay.dev/graphql/connections.htm) model to handle pagination.

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

Following the same API fetching logic, you can retrieve data for a single product.

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
## Managing product data

You can manage catalog data using the BigCommerce's [Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api). To retrieve the complete list of products, send a `GET` request to `/v3/catalog/products`. If you need to influence the response, optional query string parameters can be passed with the request. We recommend caching the product data and storing it in a database to improve performance.

```http
GET https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}
``` 

## Using the Pricing API

**Overview Pricing** is the mode of pricing used on the storefront to generate a starting price of an item before a shopper applies any customization to it.

The [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing) allows you to fetch **Overview Pricing** for a product and its selections or variants based on the shopper’s currency, customer group, and the channel they are shopping from. 

Using the [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing), you can calculate the pricing displayed for a particular channel or a customer group on your storefront.

To calculate the price for each of the sellable items on the page, supply their product IDs (required) and variant IDs (optional) in a `POST` request to `/v3/pricing/products`.

The following example shows how to call the Pricing API.

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

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

> ### Note
> The Pricing API is best suited for specific use cases that are only concerned with pricing. 

</div>
</div>
</div>

When building your own storefront, we recommend using the GraphQL Storefront API to consume the product data as it can retrieve pricing and other product-related information in a single call and orchestrate an aggregated response.

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
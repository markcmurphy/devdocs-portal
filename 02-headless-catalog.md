# Catalog

<div class="otp" id="no-index">

### On this Page	
- [Rendering Pages](#rendering-pages)
- [Managing Product Data](#managing-product-data)
- [Best Practices](#best-practices)
- [Next Steps](#next-steps)
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

The following example demonstrates how to fetch product data using the GraphQL Storefront API. It follows the GraphQL Cursor Connections Specification model and shows a simple GraphQL query for a store's products.

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
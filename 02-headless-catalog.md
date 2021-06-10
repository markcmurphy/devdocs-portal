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

## Rendering pages

Before you can display products on a headless storefront, you need to create a channel and a channel site for that storefront. A channel is essentially a sales platform such as a headless storefront, a marketplace, or a POS system. A site is a domain that links a headless storefront to a sales channel.

You can create both using the [Channels API](https://developer.bigcommerce.com/api-reference/store-management/channels). 

Start by sending a `POST` request to the `/channels` endpoint to create a channel for your headless platform. Retrieve the channel ID returned in the response. You will use it to create a channel site. 

Next, pass that channel ID in a `POST` request to `/channels/{channel_id}/site` to create a site for the provided channel. 

Now that you have set up your channel, you can implement authentication. To authenticate cross-origin requests, [create a JWT token](https://developer.bigcommerce.com/api-reference/storefront/graphql#tokens-via-api) through the Storefront API. 


## Managing product data

**Override pricing using the Pricing API**

The [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing) lets you override product pricing for a specific channel or a customer group. To override the price for each of the sellable items on the page, supply their product IDs (required) and variant IDs (optional) in a `POST` request to `/v3/pricing/products`.

The following example illustrates how to assign pricing for a number of items using the customer group pricing.

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

**Response**

```json
{
  "data": [
    {
      "bulk_pricing": [],
      "calculated_price": {
        "as_entered": 57.97,
        "entered_inclusive": false,
        "tax_exclusive": 57.97,
        "tax_inclusive": 62.75
      },
      "minimum_advertised_price": null,
      "options": [],
      "price": {
        "as_entered": 57.97,
        "entered_inclusive": false,
        "tax_exclusive": 57.97,
        "tax_inclusive": 62.75
      },
      "price_range": {"maximum": {...}, "minimum": {...}},
      "product_id": 77,
      "reference_request": {"product_id": 77},
      "retail_price": null,
      "retail_price_range": {"maximum": {...}, "minimum": {...}},
      "sale_price": null,
      "saved": null,
      "variant_id": null
    },
    {...},
    {...},
    {...}
  ],
  "meta": {}
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
# Catalog

<div class="otp" id="no-index">

### On this Page	
- [Rendering Pages](#rendering-pages)
- [Manaaging Product Data](#managing-product-data)
- [Best Practices](#best-practices)
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>


You can use BigCommerce's [Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api) to request product data to display on your Product Details and Product Listing pages.

## Rendering Pages

To retrieve the complete list of products, send a `GET` request to `/v3/catalog/products`. You can pass optional query string parameters to influence the response. We recommend caching the product data and storing it in a database to increase performance efficiency.

```http
GET https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products
Accept: application/json
Content-Type: application/json
X-Auth-Token: {{ACCESS_TOKEN}}

``` 

Once you have fetched the product data, you can create a Product Listing page and, using the [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing), control the pricing displayed for a particular channel or a customer group on your storefront.

**Display product data on the Product Details Page**

To display select product information on a product page, you will need to first retrieve the product details. You can request specific product information by sending a `GET` request to the `/v3/catalog/products/{product_id}` endpoint and passing the desired sub-resources as query parameters.

```shell
curl --request GET \
  --url 'https://api.bigcommerce.com/stores/{store_hash}/v3/catalog/products/86?include=variants%2C%20primary_image%2C%20options' \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --header 'x-auth-token: x-auth-token'
```
**Response**

```json
{
  "data": {
    "availability": "available",
    "availability_description": "",
    "base_variant_id": 66,
    "bin_picking_number": "",
    "brand_id": 0,
    "calculated_price": 225,
    "categories": [...],
    "condition": "New",
    "cost_price": 0,
    "custom_url": {...},
    "date_created": "2015-07-03T18:16:02+00:00",
    "date_modified": "2021-04-27T15:40:17+00:00",
    "depth": 10,
    "description": "<p>Made in the USA</p> <p>Measures 20.3 x 15.2 cm / 8 in x 6 in</p> <p>Capacity 946 ml / 32 oz.</p>",
    "fixed_cost_shipping_price": 0,
    "gift_wrapping_options_list": [],
    "gift_wrapping_options_type": "any",
    "gtin": "",
    "height": 10,
    "id": 86,
    "inventory_level": 0,
    ...
    "mpn": "",
    "name": "[Sample] Able Brewing System",
    ...
    "price": 225,
    "price_hidden_label": "",
    "primary_image": {...},
    "product_tax_code": "",
    "related_products": [-1],
    "retail_price": 0,
    "reviews_count": 0,
    "reviews_rating_sum": 0,
    "sale_price": 0,
    "search_keywords": "",
    "sku": "ABS",
    "sort_order": 0,
    "tax_class_id": 0,
    "total_sold": 2147483647,
    "type": "physical",
    "upc": "",
    "variants": [{...}],
    ...
  },
  "meta": {}
}
```

## Managing Product Data

**Override pricing using the Pricing API**

The [Pricing API](https://developer.bigcommerce.com/api-reference/store-management/pricing) lets you override product pricing for a specific channel and customer group. To override the price for each of the items on the page, supply the product IDs (required) and variant IDs (optional) in a `POST` request to `/v3/pricing/products`.

The following example illustrates how to override pricing for a specific customer group ID.

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

It is best practice to cache product details in a database to improve data retrieval and increase efficiency. Caching product information will allow you to implement the search feature and control the information displayed to customers. 

**Return real-time product data**

If your catalog is changing all the time, you can use the Catalog API to return real time product information.

**Return real-time pricing and inventory data**

If you prefer working with a local copy of your data, but want to make sure that high priority pieces of data like pricing and inventory are always up to date, you can consider a hybrid model. A hybrid model would cache only certain product details and pull the other information in real time.

## Next Steps
* [Learn how to create carts headlessly]().

## Resources
* [Catalog API Overview](https://developer.bigcommerce.com/api-docs/store-management/catalog/catalog-overview)
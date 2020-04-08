# Price Lists

<div class="otp" id="no-index">

### On this Page	
- [Price Lists](#price-lists)
- [Price Lists Assignments](#price-lists-assignments)
- [Price Lists Records](#price-lists-records)

</div>

## Introduction

|Resource / Endpoint|Description|
|-|-|
|Price Lists|Create and manage catalog pricing variations|
|Price List Assignments|Assign price lists to Channels|
|Price List Records|Create and manage price list records|

### Price List Definitions

`Price List` – A collection of price records. `Price Records` make up a price list.

`Price Record` – A price override for a particular variant - minimally, this is a variant ID, price, and currency.

`PriceRecordBatch` – A way to update several `Price Records` in a `Price List` at once. Using this bulk upsert endpoint, you can upsert up to 1000 Price Records in a single API call.

`Currency` – A `Price List` can contain records for multiple currencies. At this time, only price records that match the store’s default currency will be used to determine storefront and in-cart prices. Although BigCommerce supports a storefront currency selection, this is not currently integrated with Price Lists and will merely convert prices from the store’s default currency for display convenience.

## Price Lists

A Price List allows you to populate different versions of catalog pricing and assign them to different [Customer Groups](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api). 

The prices are specified exclusively at the variant level. If an active Price List does not contain prices for a variant then the Catalog pricing will be used. 

|Resource / Endpoint|Description|
|-|-|
|[`Get All Price Lists`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/getpricelistcollection)|Returns a list of Price Lists|
|[`Create a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/createpricelist)|Creates a Price List|
|[`Delete All Price Lists`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/deletepricelistsbyfilter)|Deletes all Price Lists|
|[`Get a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/getpricelist)|Returns a single Price List|
|[`Update a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/updatepricelist)|Updates a Price List|
|[`Delete a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/deletepricelist)|Deletes a Price List|

## Price Lists Assignments

A Price List Assignment can be created to assign a Price List to a specific sales Channel. This association lets you define custom pricing for shoppers only on a specific external site or platform. Price List Assignments can be combined with a Customer Group assignment to more specifically target logged in customers shopping on that Channel.


### Usage Notes
* The association of a Price List to a Customer Group can be done either via the Control Panel or using the [Customer Groups API](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api).
* Price Lists cannot be assigned to a Customer Group that has custom group discounts -- the customer group discounts must be deleted first.

### Order of Operations

The `Price List Assignment` Pricing Order of Operations is as follows:

**IF** `Price list` assigned to current `Customer Group` **AND** `Price List` assigned to current `Channel`:
* Use this price list -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

**ELSE IF**: `Price List` assigned to current `Channel`:
* Use this price list -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

**ELSE IF** `Price List` assigned to current `Customer Group`:
* Use this price list -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

**ELSE IF** `Customer Group Discounts`:
* Use them -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

**ELSE IF** `channel` has a `default price list`:
* Use this price list -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

**ELSE**:
* Fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

|Resource / Endpoint|Description|
|-|-|
|[`Create Price List Assignments`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists-assignments/createpricelistassignments)|Creates a batch of Price List Assignments|
|[`Get Price List Assignments`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists-assignments/getlistofpricelistassignments)|Returns a list of Price List Assignments|
|[`Delete Price List Assignments`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists-assignments/deletepricelistassignmentsbyfilter)|Deletes one or more Price List Assignments|

## Price Lists Records

### Usage Notes
* Bulk Pricing Tiers may additionally be associated with a Price Record to indicate different pricing as the quantity in cart increases.
* If a variant has a `Price Record` any existing product-level bulk pricing will not apply in the cart. For variants without `Price Records`, any existing product bulk pricing will apply.
* Price Lists Records accepts bulk upsert. Only one [Bulk upsert](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/setpricelistrecordcollection) can done at a time. Running more than one in parallel on the same store will cause a 429 error and the request will fail.

|Resource / Endpoint|Description|
|-|-|
|[`Get All Price List Records`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/getpricelistrecordcollection)|Returns a list of Price List Records|
|[`Upsert Price List Records`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/setpricelistrecordcollection)|Updates Price List Records|
|[`Delete a Price List Record`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/deletepricelistrecordsbyfilter)|Deletes a Price List Record|
|[`Get Price Records by Variant`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/getpricelistrecordsbyvariantid)|Returns Price List Records using the variant ID|
|[`Get a Price Record by Currency Code`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/getpricelistrecord)|Returns a Price List Record using the currency code|
|[`Set Price List Record by Currency Code`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/setpricelistrecord)|Creates or updates a Price List Record using the currency code|
|[`Delete a Price List Record by Currency Code`](https://developer.bigcommerce.com/api-reference/catalog/pricelists-api/price-lists-records/deletepricelistrecord)|Deletes a Price List Record using the currency code|

### Pricing Order of Operations

The table below lists out each price type available on a product. The table is read from top to bottom with the default price having the lowest weight and the tax having the highest weight when calculating price.  

| Price Type | Description | Notes |
|--|--| --|
| Default Product Price | Required on product  |  |
| Product Sale Price | Optional on product. | Overrides default price.|
| Variant Price | Optional on product. | Overrides product sale price |
| Variant Sale Price | Optional on product.| Overrides variant price. |
| Customer Group Discount | Available in Fixed ($5), Relative (-$2), or Percentage (-25%). Might apply to one product, category, subcategory or the entire store's products. | Overrides variant sale price. |
| Product Bulk Pricing | Available in Fixed ($5), Relative (-$2), or Percentage (-25%). Dependent on total quantity of the product including SKUs added to cart. | Overrides customer group discount. |
| | <p style="text-align:center;font-weight:bold;">Price Lists override all previous pricing</p> | |
| Price List Variants | Required for a price list record.  | Overrides all previous pricing and excludes SKUs from the total number of items for product bulk pricing. |
| Price List Variant Sale Price | Optional on product. Overrides if variant pricing is set and selected. | Overrides price list pricing. |
| Price List Variant Bulk Pricing | Available in Fixed ($5), Relative (-$2), or Percentage (-25%). Dependent on quantity added to cart. | Overrides price list sale price on variants |
| Price List Variant with Product Pick List | The Product Pick List is configured to change the price when a Pick List Item is selected. | Overrides price list bulk pricing | 
| Product with Modifier | Optional on product. A modifier includes choices such as add $5 for insurance. Can be fixed ($5) or percentage (%10) to add or remove from total product price | Overrides price list with a product pick list |
| Product with a Product Pick List | If the product pick list is configured to change the price, it will update the price when the option is selected. | Overrides product with modifier |
| | <p style="text-align:center;font-weight:bold;">Cart</p>||
| Cart Level Discounts | Cart Level Discounts apply automatically when the shopper meets certain conditions or takes certain actions. | Modifies the final product or cart price depending on the discount type. |
| Coupons | Coupons require customer action to take effect. | Modifies the final product or cart price depending on the coupon type. |
| Tax | Products can be assigned to a different tax class, which will change the final amount the shopper pays. | Tax is the last to calculate after shipping and promotions are applied. |

### Stencil Storefront

Price Lists will provide overridden price values to the Stencil storefront. Final price display can be further customized within the Stencil template. See the [Price Object](https://developer.bigcommerce.com/stencil-docs/reference-docs/common-objects#price) in Stencil for further documentation.

### Webhooks
There are no direct webhooks available for Price Lists. Since Price Lists directly relate to products, webhooks related to products will fire for corresponding changes such as pricing.

* [Products](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_products)
* [SKU](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_sku)

### Resources

[Price List API](https://developer.bigcommerce.com/api-docs/catalog/price-list-overview)

[Price Order of Operations](https://developer.bigcommerce.com/api-docs/catalog/pricing-order-operation)

[Catalog Price Object Examples](https://developer.bigcommerce.com/stencil-docs/developing-further/catalog-price-object)

[Common Stencil Objects: Price](https://developer.bigcommerce.com/stencil-docs/reference-docs/common-objects#price)
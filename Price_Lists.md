# Price Lists

<div class="otp" id="no-index">

### On this Page	
- [Price Lists](#price-lists)
- [Price Lists Assignments](#price-lists-assignments)
- [Price Lists Records](#price-lists-records)

</div>

## Introduction

A Price List allows you to populate different versions of catalog pricing and assign them to different [Customer Groups](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api). The prices are specified exclusively at the variant level.

If an active Price List does not contain prices for a variant then the Catalog pricing will be used. The association of a Price List to a Customer Group can be done either via the Control Panel or using the [Customer Groups API](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api).

Price Lists will provide overridden price values to the Stencil storefront. Final price display can be further customized within the Stencil template. See the [Price Object](https://developer.bigcommerce.com/stencil-docs/reference-docs/common-objects#price) in Stencil for further documentation.

To learn more about Price Lists, see [here](https://developer.bigcommerce.com/api-docs/catalog/price-list-overview).

## Price Lists

|Resource / Endpoint|Description|
|-|-|
|[`Get All Price Lists`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/getpricelistcollection)|Returns a list of Price Lists|
|[`Create a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/createpricelist)|Creates a Price List|
|[`Delete All Price Lists`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/deletepricelistsbyfilter)|Deletes all Price Lists|
|[`Get a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/getpricelist)|Returns a single Price List|
|[`Update a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/updatepricelist)|Updates a Price List|
|[`Delete a Price List`](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists/deletepricelist)|Deletes a Price List|

## Price Lists Assignments

Price List Assignments can be created to assign Price Lists to a specific Channel. Price lists assigned to a channel apply to all shoppers on that channel, unless there is a more specific assignment.

### Usage Notes
Price Lists cannot be assigned to a customer group that has custom group discounts -- the customer group discounts must be deleted first.

### Order of Operations

The `Price List Assignment` Pricing Order of Operations is as follows:

**IF** `Price list` assigned to current `Customer Group` **AND** `Price List` assigned to current `Channel`:
* Use this Price List -- any prices not found fall back to the catalog price (or in the case of multi-currency, auto-converted prices)

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

### Webhooks
There are no direct webhooks available for Price Lists. Since Price Lists directly relate to products, webhooks related to products will fire for corresponding changes such as pricing.

* [Products](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_products)
* [SKU](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_sku)

### Resources

[Catalog Price Object Examples](https://developer.bigcommerce.com/stencil-docs/developing-further/catalog-price-object)

[Common Stencil Objects: Price](https://developer.bigcommerce.com/stencil-docs/reference-docs/common-objects#price)
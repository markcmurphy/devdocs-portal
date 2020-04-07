# Price Lists

<div class="otp" id="no-index">

### On this Page	
- [Price Lists](#price-lists)
- [Price Lists Assignments](#price-lists-assignments)
- [Price Lists Records](#price-lists-records)

</div>

## Introduction

A Price List allows you to populate different versions of catalog pricing and assign them to different [Customer Groups](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api). The prices are specified exclusively at the variant level.

The association of a Price List to a Customer Group can be done either via the Control Panel or using the [Customer Groups API](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api).

Additionally, [Price List Assignments](https://developer.bigcommerce.com/api-reference/store-management/price-lists/price-lists-records/) can be created to assign Price Lists to a specific [Channel](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api). Price lists assigned to a channel apply to all shoppers on that channel, unless there is a more specific assignment.

If an active Price List does not contain prices for a variant then the Catalog pricing will be used. The association of a Price List to a Customer Group can be done either via the Control Panel or using the [Customer Groups API](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api).

Price Lists will provide overridden price values to the Stencil storefront. Final price display can be further customized within the Stencil template. See the Price Object in Stencil for further documentation.

To learn more about Price Lists, see [here](https://developer.bigcommerce.com/api-docs/catalog/price-list-overview).

## Price Lists

## Price Lists Assignments

## Price Lists Records

### Resources

[Catalog Price Object Examples](https://developer.bigcommerce.com/stencil-docs/developing-further/catalog-price-object)

[Theme Docs: Blog](https://developer.bigcommerce.com/stencil-docs/reference-docs/other-objects-and-properties-overview#blog)
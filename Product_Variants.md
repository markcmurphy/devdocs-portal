## Product Variants

[Variants](/api-reference/catalog/catalog-api/product-variants/getvariantsbyproductid) represent an item as it sits on the shelf in the warehouse or a particular saleable product. A product might be a t-shirt, while the variant would be “a small, red t-shirt”. Variants are selected by shoppers on the storefront via Product Options. In the case where a product is simple, meaning it does not have any options, the product is its own variant - called a base variant. Everything you can buy should be a variant.

* Options build out variants.
* Variants are usually what inventory is tracked against
* Can have their own price, weight, dimensions, image, etc - or they can inherit these values from the product if they have not been specified
* Must have a SKU code (unless they’re a base variant)
* In the case of non-base variants, variants will relate to a particular combination of variant option values - such as “small” and “red”

| If the product is | Variant Option | Variant |
| -- | -- | -- |
| T-Shirt | Blue<br>-<br> Small<br> Medium<br> Large| SM-BLU<br> SM-MED <br> SM-LARG
| Backpack | Black<br>Yellow<br>-<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L<br>-<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L|

## Product Variant Metafields

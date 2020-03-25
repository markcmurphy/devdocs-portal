## Product Modifiers

[Modifier options](/api-reference/catalog/catalog-api/product-modifiers/getmodifiers) are any choices that the shopper can make that will change the way the merchant fulfills the product. Examples include:
* A checkbox to add shipping insurance
* Text to be engraved on the product
* A color that an unfinished product is to be painted before it’s shipped

Critically, the modifier will not change the SKU/variant being fulfilled, and you cannot track inventory against combinations of modifier values. Modifiers typically would not change which product is “picked off the shelf” in the warehouse, but they change what happens to that product before it’s sent to the shopper, or how it’s sent.

Modifier options:
* May be required or non-required
* Support all option types
* Cannot be used as part of a variant

An adjuster can be added to a modifier option to change things such as increasing the price, changing the weight, or shipping rules.  Adjusters cannot be applied to all modifier types.

### Modifier Options Example:

| If the product is | Variant Option | Variant |Modifier |
| -- | -- | -- | -- |
| T-Shirt | Blue<br>-<br> Small<br> Medium<br> Large| SM-BLU<br> SM-MED <br> SM-LARG| Checkbox<br>Donate to Charity|
| Backpack | Black<br>Yellow<br>-<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L<br>-<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L| Text Field<br> Add Embroidery|

> **Modifiers that require a second step to add an adjuster**
> Swatch, radio buttons, drop-down, rectangle list, product list, product list with images, and checkbox.

## Product Modifier Images

## Product Modifier Values

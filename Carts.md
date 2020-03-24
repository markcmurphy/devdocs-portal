## Carts

## Abandoned Carts

## Cart Items 

## Cart Redirect URIs


### Troubleshooting Cart Errors

We will go over common Server-to-Server Cart errors. 

**Please create some text for the API option [422]**

*Issue*: When a cart is created containing a product that has an incorrect or missing text modifier.

*Resolution*: Options and modifiers refer to a list of choices on a product. Options are used to build out variants and modifiers are not tied to variants at all. To learn more about options and modifiers see [Products Overview](https://developer.bigcommerce.com/api-docs/catalog/products-overview#products-overview_modifier-options).

*Single Modifier*

To add a product to the cart that has a single modifier (text field), POST to the [Cart API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/createacart) without the `variant_id`.

*Single Option*

To add a product to the cart that has one option (radio button) associated with it, use just the `variant_id` in the request.

*Modifier and Option*

To add a product that has both an option and a modifier associated with it, then use the `option_id` and `option_value`. 

**Missing line_items in request body [422]**

[Handlebars Reference](https://developer.bigcommerce.com/stencil-docs/reference-docs/global-objects-and-properties/cart)

{{cart}}

Note: Server-to-Server only, not Storefront

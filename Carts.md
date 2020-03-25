## Carts

Server-to-Server Cart API allows for a cart to be created using BigCommerce cart logic. The existing BigCommerce front-end cart can be bypassed.

A cart contains a collection of items, prices, discounts, etc. It does not contain customer-related data.

**Notes:**

* A cart can be creted using an existing catalog item or by adding a custom item. 
* `cartId` is the same as the `checkoutId`.
* Carts are valid for 30 days from the last modification. This includes creating the cart or editing the cart.
* If a product has modifiers, omit the `variant_id` and instead use the `option_selections` array to describe both the variant and the modifier selections.
* Changing the Cart `customer_id` will remove any promotions or shipping on the Cart. These are tied to the customer depending on cart conditions and any customer groups.

**Guest Cart**

A guest cart assumes the shopper is not a customer and is not logging in or creating an account during checkout. Guest checkouts should be handled by displaying the cart data to the customer and then moving them to Checkout using the [Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api). 

|Resource / Endpoint|Description|
|-|-|
|[`Create a Cart`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/createacart)|Creates a Cart|
|[`Get a Cart`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/getacart)|Returns a stored Cart|
|[`Update a Cart`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/updateacart)|Updates a Cart's `customer_id`|
|[`Delete a Cart`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/deleteacart)|Deletes a Cart|

**Persistent Cart**

Persistent Cart allows for a logged in shopper to access the same cart across devices. Persistent Cart is available on Plus, Pro, and Enterprise plans.

Persistent Cart works with the Storefront Cart and Server-to-Server Cart APIs. To learn more, see [Persistent Cart](https://support.bigcommerce.com/s/article/Persistent-Cart). 

## Abandoned Carts

Use `/abandoned-carts/{token}` on headless storefronts to retrieve the `cartId` via the abandoned cart token passed in to headless storefront via an abandoned cart email link clicked on by a shopper. Once the `cartId` has been retrieved, it can be used to fetch and display information about the cart to the shopper via the Storefront Cart and/or Server-to-Server Cart APIs.

`{token}` is the token in the query string of the abandoned cart link found in the abandoneed cart email notifications to shoppers. 

|Resource / Endpoint|Description|
|-|-|
|[`Get an Abandoned Cart`](https://developer.bigcommerce.com/api-reference/cart-checkout/s2s-abandoned-carts/abandoned-carts/getabandonedcarts)|Returns a `cartId` corresponding to the abandoned cart `token`|

## Cart Items 

A list of items added to the cart in the current session.

To add a custom item, use `custom_items`.

|Resource / Endpoint|Description|
|-|-|
|[`Add Cart Line Items`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart-items/addcartlineitem)|Adds a Line Item to the Cart|
|[`Update Cart Line Item`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart-items/updatecartlineitem)|Updates a Cart Line Item|
|[`Delete Cart Line Item`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart-items/deletecartlineitem)|Deletes a Cart Line Item|

## Cart Redirect URLs

A Cart Redirect URL is used to redirect a shopper to an already created cart using the `cartId`.

Redirect URLs can only be generated from carts created using the Server-to-Server Cart API. The `cartId` is used to generate a `redirect_url`. 

To get cart `redirect_urls` in the response, append the `include=redirect_urls` query parameter to the request URL.

To restore a cart that was created on the storefront, either by a shopper or the Storefront Cart API, recreate the cart using the Server-to-Server Cart API.

|Resource / Endpoint|Description|
|-|-|
|[`Create Cart Redirect URL`](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart-redirect-urls/createcartredirecturl)|Creates a Cart Redirect URL|

**Custom Add to Cart URLs**

See [Add to Cart URLs](https://developer.bigcommerce.com/api-docs/cart-and-checkout/add-to-cart-url) for more information. 

Query string parameters can be appended to BigCommerce product and `/cart.php` urls in order to pre-select an SKU or add a product to cart. These parameters make it possible to build custom add to cart links and forms for use on BigCommerce storefronts and remote sites (such as WordPress, blog posts, and social media).

URLs constructed with these parameters can be used to:

* Pre-select a specific SKU on a product detail page
* Add a specific product or SKU to the cart
* Add a specific SKU to the cart and go directly to checkout.
* Attach a `source` for marketing an analytics purposes

**Parameters**

| **Type**| **Parameter** | **Description**                                     | **Example**                                                 |
|-- |-|--|-|
| string  | `action=`     | `add` or  `buy`; `buy` goes directly to checkout    | `/cart.php?action=add&product_id=123`                       |
| string  | `couponcode=` | coupon code to apply to the cart                    | `/cart.php?action=add&product_id=123&couponcode=10off100`   |
| int     | `product_id=` | product id to add to the cart                       | `/cart.php?action=add&product_id=123`                       |
| int     | `qty=`        | quantity to add to the cart                         | `/cart.php?action=add&product_id=123&qty=3`                 |
| string  | `sku=`        | SKU to add to the cart (or select on product page)  | `/cart.php?action=add&sku=xlredtshirt`                      |
| string  | `source=`     | source of the sale for analytics; can be any string | `/cart.php?action=buy&sku=xlredtshirt&source=emailcampaign` |

**Common Usage**

Below is a table of common scenarios and example URLs.

| **Scenario**                                                 | **URL**                                                              |
|--|-|
| Select a specific SKU on Product Detail page                 |`https://{{domain}}/{{page}}?sku={{sku}}`                             |
| Add specific SKU to cart                                     |`https://{{domain}}/cart.php?action=add&sku={{sku}}`                  |
| Add specific SKU to cart, go directly to checkout            |`https://{{domain}}/cart.php?action=buy&sku={{sku}}`                  |
| Add specific SKU to cart, go to checkout, and include source |`https://{{domain}}/cart.php?action=buy&sku={{sku}}&source={{src}}`   |
| Add product to cart by product id and set quantity           |`https://{{domain}}/cart.php?action=add&product_id={{id}}&qty={{qty}}`|
| Add product to cart and set coupon code                      |`https://{{domain}}/cart.php?action=add&couponcode={{code}}`          |

Once constructed, a URL can be inserted directly as text or as an HTML link:

```html
<a href="https://example.com/cart.php?action=buy&product_id=123&source=blogpost">Purchase Our New Product Now!</a>
```

**Adding Multiple Products**

The `sku` and `product_id` parameters accept a single value; if a comma separated list of values is passed in, only the first value is used. In other words, only one product can be added for each request made to an add to cart URL.

Although it is possible to combine several HTTP requests into a single button click using JavaScript, this method is limited to the BigCommerce storefront. Depending on the complexities and specifics of the use case, the [Storefront Cart API](https://developer.bigcommerce.com/api-docs/cart-and-checkout/working-sf-apis) may be a more suitable option. 

### Troubleshooting Cart Errors

We will go over common Server-to-Server Cart errors. 

**Please create some text for the API option [422]**

*Issue*: When a cart is created containing a product that has an incorrect or missing text modifier.

*Resolution*: Options and modifiers refer to a list of choices on a product. Options are used to build out variants and modifiers are not tied to variants at all. To learn more about options and modifiers see [Products Overview](https://developer.bigcommerce.com/api-docs/catalog/products-overview#products-overview_modifier-options).

*Single Modifier*

To add a product to the cart that has a single modifier (text field), POST to the [Cart API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api/cart/createacart) without the `variant_id`.

*Single Option*

To add a product to the cart that has one option (radio button) associated with it, use the `variant_id`.

*Modifier and Option*

To add a product that has both an option and a modifier associated with it, use the `option_id` and `option_value`. 

**Missing line_items in request body [422]**

*Issue*: When a required product modifier is missing. A product can have a modifier that is not required. In those cases the product can be added to a cart without the modifier.

*Resolution*: Use the [Get Products](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/products/getproducts) or [Get Modifier](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/product-modifiers/getmodifiers) endpoints to return the modifier ID. The `modifier_id` = `option_id`.

**A shipping address for this order is incomplete [422]**

*Issue*: This can return when the customer ID of a cart has changed.

*Resolution*: The customer ID is linked to discounts and pricing available to that customer. If that is changed then anything that affects the cart price is invalidated. This includes coupons, discounts, taxes and shipping.

A cart should be created with the `customer_id` as part of the request body. Use the [Get Customers](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customers/getallcustomers) endpoint to get the `customer_id`.

**This product has options, variant ID is required [422]**

*Issue*: When a product has options and variant ID is not supplied in either the create or update cart request.

*Resolution*: To get the variant ID use the [Get Products](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/products/getproducts) endpoint or the [Get Variants](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/product-variants/getvariantsbyproductid) endpoint. 

**You can only purchase a maximum of :qty of the :product per order [409]**

*Issue*: When less than a product’s minimum required purchase or more than the maximum allowed purchase is added to cart.

*Resolution*: Check the product for `order_quantity_minimum` and `order_quantity_maximum` for the correct amount to add the cart. Use the [Get Product](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/products/getproducts) endpoint.

**Internal Server Error [500]**

*Issue*: Trying to edit a Cart that does not exist.

*Resolution*: Carts are only valid 30 days past the `date_last_modified`. Check the [Get Carts](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-cart-api/cart/getacart) endpoint for the current available session cart.

[Cart Webhook Events](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_cart)

[Theme Docs](https://developer.bigcommerce.com/stencil-docs/reference-docs/other-objects-and-properties-overview#cart)

[Handlebars Reference](https://developer.bigcommerce.com/stencil-docs/reference-docs/global-objects-and-properties/cart)

[Help Center: Persistent Cart](https://support.bigcommerce.com/s/article/Persistent-Cart)

[Help Center: Using the Abandoned Cart Saver](https://support.bigcommerce.com/s/article/Using-the-Abandoned-Cart-Saver)

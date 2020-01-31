# Title

<div class="otp" id="no-index">

### On this Page	
- [Supported Templates](#supported-templates)
- [Global](#global)
- [Category](#category)
- [Blog](#blog)
- [Brand](#brand)
- [Brand List](#brand-list)
- [Cart](#cart)
- [Search](#search)

</div>

YAML Front Matter reference for BigCommerce Stencil themes.

## Supported Templates

YAML Front Matter is supporte for templates in the `templates/pages/` directory.

Front Matter is not supported for templates in the following directories:
* `templates/components/`
* `templates/layout/`
* `templates/pages/custom/`

## Global

**Availability:** All Pages

```yaml
customer:                        # customer specific settings             
  returns: true                  # show product-return requests for this customer?
  wishlists:     
    limit: 10                    # limit the number of wishlists to 10
  orders:
    limit: 10                    # limit the number of orders displayed to 10
  recently_viewed_products: true # display recently viewed productS?
```

|  Property | Description |
| --- | --- |
|  `customer` | Customer attributes are always included, and are available if the active shopper is logged in. |
|  `returns` | Boolean indicating whether to retrieve product-return requests for this customer. No filtering available.true: Retrieve requests. null or false: Do not retrieve requests. |
|  `wishlists` | If `null`, wishlists displayed. If `limit` not specified, retrieves unlimited number of wishlists. |
|  `orders` | If `null`, no orders displayed. Displays complete and incomplete orders.If `limit` not specified, displays 20 orders |
|  `recently_viewed_products` | Boolean indicating whether to display recently viewed products. No filtering avaiable. |
|  `limit` | The maximum number of the entity to display. |

## Category
Content

## Blog
Content

## Brand
Content

## Brand List
Content

## Cart
Content

## Search
Content 
<div class="otp" id="no-index">

### On this Page	
- [Coupons](#Coupons)
- [Section2](#section2)
- [Section3](#section3)

</div>

## Coupons
Category or product discounts that can be applied to orders for customers who enter a given code.

|Resource / Endpoint|Description|
|-|-|
|[`Get All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getallcoupons)|Returns a list of Coupons|
|[`Create a Coupon`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/postcoupons)|Creates a new coupon|
|[`Get All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getallcoupons)|Returns a list of Coupons|
|[`Get All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getallcoupons)|Returns a list of Coupons|
|[`Get All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getallcoupons)|Returns a list of Coupons|
**Notes**
* Default sorting is by coupon/discount id, from lowest to highest. Optional filter parameters can be passed in.

* Available types for `type` and `exclude_type` filters:

|Type|
|-|
|`per_item_discount`|
|`percentage_discount`|
|`per_total_discount`|
|`shipping_discount`|
|`free_shipping`|
|`promotion`|

* Coupons with `type=promotion` will not populate usable data for the following fields but instead be set to the following default values:

```json
...
amount : 0.0000
min_purchase: 0.0000
applies_to
restricted_to: []
shipping_methods : null
...
```
<div class="otp" id="no-index">

### On this Page	
- [Coupons](#Coupons)
- [Promotions Coupons](#promotions-coupons)
- Resources

</div>

## Coupons (V2)
A coupon is a category or product discount that can be applied to orders for customers who enter a given code at checkout.

Only one coupon can be used per order.

|Resource / Endpoint|Description|
|-|-|
|[`Get All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getallcoupons)|Returns a list of Coupons.|
|[`Create a Coupon`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/postcoupons)|Creates a new coupon.|
|[`Delete All Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/deleteallcoupons)|By default, it deletes a page of Coupons.|
|[`Get A Count of Coupons`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/getacountofcoupons)|Returns a count of all Coupons in the store.
|[`Delete a Coupon`](https://developer.bigcommerce.com/api-reference/store-management/marketing/coupons/deleteacoupon)|Deletes a Coupon.

**Notes**

Default sorting is by coupon/discount id, from lowest to highest. Optional filter parameters can be passed in.

Available coupon types for `type` and `exclude_type` filters:

|Type|Description|
|-|-|
|`per_item_discount`|Dollar amount off each item in the order|
|`percentage_discount`|Percentage off each item in the order|
|`per_total_discount`|Dollar amount off the order total (subtotal)|
|`shipping_discount`|Dollar amount off the shipping total|
|`free_shipping`|Free shipping|

If the `applies_to` value is cleared, you can restore it to the coupon by reapplying the `applies_to` value in a new PUT request.

Only the following fields can be updated via `PUT`:

* `code`
* `max_uses`
* `max_uses_per_customer`

Coupons with `type=promotion` will not populate usable data for the following fields but instead be set to the following default values:

```json
...
amount : 0.0000
min_purchase: 0.0000
applies_to
restricted_to: []
shipping_methods : null
...
```
## Promotions Coupon (V3)
Coupons can also be created via the Promotions API (Beta). These Coupons can be used to offer discounts if shoppers meet specific conditions. The conditions available are the same as those that can be set with
[Automatic Promotions](https://support.bigcommerce.com/s/article/Automatic-Promotions) (Beta).

**Limitations**
* Cannot be restricted by location
* Cannot be restricted by shipping method
* You cannot exclude them from being used with Automatic Promotions










<div class="otp" id="no-index">

### On this Page	
- [Sites and Routes](#sites-and-routes)
- [Related Articles](#related-articles)

</div>

## Sites and Routes
The Sites and Routes APIs let you set an external storefront domain  and define the paths for important pages, like the home page, cart page, or checkout page. The site and routes are used to link back to the proper URL from invoice emails and storefront links.

The following route types are currently supported. (meaning we will redirect shoppers back to given routes for these):

* Type: “home”
* Type: “product”
* Type: “cart”
* Type: “checkout”
* Type: “account_order_status” (for order statuses on an account)
* Type: “account_new_return” (for returns on an account)
* Type: “unsubscribe” (for unsubscribe URL in emails)
* Type: “recover_abandoned_cart” (for URL in emails for a shopper to recover their abandoned cart)
* Type: “create_account”
* Type: “forgot_password”
* Type: “order_confirmation” (supported in future update to override order confirmation page)


**Notes**
- When updating an existing route, you must provide the id in the route object.

## Related Articles
https://developer.bigcommerce.com/api-docs/cart-and-checkout/embedded-checkout/embedded-checkout-tutorial

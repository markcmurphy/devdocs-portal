# Managing Customers

<div class="otp" id="no-index">

### On this Page	
- [Next steps](#next-steps)
- [Resources](#resources)

</div>

Introduction

## Associate cart with a customer

If a shopper creates a cart as a guest then logs into the store, you can use the following process to associate the cart to the customer and log them in at the same time. The [Server to Server Cart API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api) is used since it allows for the front end to be bypassed when creating a cart.

When a cart is created, your app should store the `cart_id`.  The `cart_id` is used to generated a `redirect_url`. Using the [Customer Login API](https://developer.bigcommerce.com/api-docs/customers/customer-login-api) set the `redirect_to` parameter as the generated cart or checkout redirect url. This will both log the customer in and show them either the cart or checkout depending on which url was used.  To make sure the cart is matched to the right customer you should compare the entered email address to what is the store’s database.

To populate the `customer_id` on the cart with the correct data, use the email address entered to match against the [Customers API](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api). If the email address matches what the customer input and what is in the BigCommerce database then proceed with login. If a match is not found then direct the customer to a [sign up](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customers/customerspost) screen.

## Next Steps
* [Learn more about {{TOPIC}}]().

## Resources
* [Link]() 
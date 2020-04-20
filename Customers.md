# Customers

<div class="otp" id="no-index">

### On this Page	
- [Customers](#customers)
- [Customer Addresses](#customer-addresses)
- [Customer Attributes](#customer-attributes)
- [Customer Attribute Values](#customer-attribute-values)
- [Customer Form Field Values](#customer-form-field-values)
- [Customer Groups](#customer-groups)
- [Customers Validate Password](#customers-validate-password)
- [Subscribers](#subscribers)

</div>

## Customers

For a comprehensive list of associated endpoints, visit the [V2 Customers](https://developer.bigcommerce.com/api-reference/store-management/customers-v2) and [V3 Customers](https://developer.bigcommerce.com/api-reference/store-management/customers-v3) reference pages. 

### What is a Customer?

A Customer is a shopper who has created an account on the storefront. Customers data is comprised of attributes about the shopper including their name, email address and physical addresses. 

### What is a Guest?
Store settings can be set to allow a shopper to complete checkout without creating an account. These shoppers are not captured as customers or stored in the BigCommerce system. If you want to capture guest data, using the Storefront APIs can help.

## V2 vs. V3

The main distinction between Customers V2 and V3 is you can only manage certain resources using either API.

V2 Customers API allows you to manage the following resources:
* Customers
* Customer Addresses
* Customer Groups
* Customer Passwords

V3 Customers API allows you to manage the following:
* Customer Addresses
* Cusrtomer Attributes
* Customer Form Fields
* Customer Consent

### Making Requests

V3 API reduces the calls needed to create and update Customers. For example, you can create customer attributes and addresses in one step, allowing batch creation of multiple customers — and their subresources — in a single API call.

**Create a Customer**

Single Customer on V3
- `/customers`

Single Customer on V2
* `/customers/{customer_id}`
* `/customers/{customer_id}/addresses`

### Queries

With the V3 Customers API, queries become a powerful tool. Instead of using a different endpoint to get customer sub-resources, there is one GET endpoint per resource with filters to refine the request. 

**Get Customer Addresses**

Get Customer Address by name and company on V3
`/customers/addresses?company:in=bigcommerce,commongood&customer_id:in1,2,3`

Get Customer Address by name and company on V2
`/customers/{customer_id}/addresses/{customer_address_id}`

### Upsert

Upsert is used for Form Field Values and Customer Attributes. Upsert looks for a match to the existing record, and if one is found, then it makes an update. If a match is not found, it creates a new record.

### Authentication Object

On the new Customers endpoint, when creating a customer there are two ways to set customers passwords. 
- A new password can be set under the `authentication > new password` object in a /PUT or /POST. 
- To have customers reset the password set `force_password_reset` to `true` under `authentication > new password` object in a /PUT or /POST

## Customer Addresses

Customer Addresses are the addresses that are associated with a Customer Account when customers enter a new billing or shipping address at checkout. They can also be set by the customer while logged in to their store account.


## Customer Attributes
Customer Attributes are a name/value key pair associated with a Customer. They are readable/writable via API only.

**Note**
<br>
Each customer can have up to 100 name, value pairs stored


## Customer Form Field Values
These are the values customers enter in form fields at checkout via [Account Sign Up Form](https://support.bigcommerce.com/s/article/Editing-Form-Fields).


## Customer Groups

Customer groups allow you to organize your customers, give them discounts, and restrict access to specific products or categories. For more information see [Customer Groups](https://support.bigcommerce.com/s/article/Customer-Groups).

**Note**
<br>
The Customer Groups feature is only available on certain plans.

## Customers Validate Password
Password validation is only available on V2 Customers API. Validation will return a true or false. The V3 Customers API can reset a customers password or input a new password. 

## Subscribers
A subscriber is someone who has signed up for a store’s newsletter.  
Subscribers can be added by:

- Signing up for the newsletter via the signup box located in the footer of most storefront themes
- Signing up for the newsletter during checkout
- POSTing to the Subscribers API

Where possible, the API indicates the origin of the subscriber. If the subscriber was added during checkout, the Order ID is included.

### Subscribers vs. Customers

- A subscriber is not always a customer. Someone can sign up for the newsletter only and not create an account.
- A customer is not always a subscriber. Signing up for the newsletter is a separate action from creating an account and purchasing an item.
- A customer and a subscriber can be the same. If a shopper checks out on the storefront, creates an account and opts into the newsletter, they are a customer and a subscriber.

## Resources

### Related Endpoints
  [Customer Login API](https://developer.bigcommerce.com/api-docs/customers/customer-login-api)
- [Current Customer API](https://developer.bigcommerce.com/api-docs/customers/current-customer-api)
- [Customers API](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api)
- [Customer Groups](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customer-groups/getallcustomergroups) (Customer V2 API)
- [Password Validation](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customer-passwords/validatecustomerpassword) (Customer V2 API)
- [Password Confirmation](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customers/createanewcustomer) (Customer V2 API)
- [Subscribers API](https://developer.bigcommerce.com/api-reference/customer-subscribers/subscribers-api)

### Webhooks
- [Customers](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_customer)

### Related Articles
- [Adding and Editing Fields in the Account Signup Form](https://support.bigcommerce.com/s/article/Editing-Form-Fields#account-fields) (Knowledge Base)
- [Checkout Settings](https://support.bigcommerce.com/s/article/Checkout-Settings#checkout-settings) (Knowledge Base)
# Customers

<div class="otp" id="no-index">

### On this Page	
- [Customers](#customers)
- [Customer Addresses](#customer-addresses)
- [Customer Attributes](#customer-attributes)
- [Customer Attribute Values](#customer-attribute-values)
- [Customer Form Field Values](#customer-form-field-values)
- [Customer Consent](#customer-consent)
- [Customer Groups](#customer-groups)
- [Customer Passwords](#customer-passwords)

</div>


For a list of associated endpoints, visit the [V2 Customers](https://developer.bigcommerce.com/api-reference/store-management/customers-v2) and [V3 Customers](https://developer.bigcommerce.com/api-reference/store-management/customers-v3) reference pages. 

## Overview

Customers APIs serve to programmatically create and manage customers and their data. 

There are two basePath properties available to the consumers of the Customers APIs:

* V2 Customers API: `/stores/{$$.env.store_hash}/v2`
* V3 Customers API: `/stores/{$$.env.store_hash}/v3`

The main distinction between the V2 and V3 Customers APIs is the resources handled by either API.

Resources that can be managed using the V2 Customers API:
* Customers
* Customer Addresses
* Customer Groups
* Customer Passwords

Resources that can be managed using the V3 Customers API:
* Customers
* Customer Addresses
* Customer Attributes
* Customer Form Fields
* Customer Consent

## Customers

### What is a Customer?

A Customer is a shopper who has created a store account. Customer data consists of such parameters as name, email, and addresses and is stored as a customer record.

### What is a Subscriber?

A subscriber is a shopper who has signed up for a store’s newsletter.

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
### Note
> Being a subscriber does not automatically make one a customer.

</div>
</div>
</div>

### Subscribers vs. Customers

- A subscriber is not always a customer. Someone can sign up for the newsletter only and not create an account.
- A customer is not always a subscriber. Signing up for the newsletter is a separate action from creating an account and purchasing an item.
- A customer and a subscriber can be the same. If a shopper checks out on the storefront, creates an account and opts into the newsletter, they are a customer and a subscriber.

To learn more about creating and managing subscribers, see [Subscribers](https://developer.bigcommerce.com/api-reference/customer-subscribers/subscribers-api). 

### What is a Guest?
Store settings can be set to allow a shopper to checkout without creating an account. These users are not captured as customers or stored in the BigCommerce system. To retrieve guest checkout data, API users may want to review [the Storefront Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/storefront-checkout-api). 

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

## Customer Consent

## Customer Groups

Customer groups allow you to organize your customers, give them discounts, and restrict access to specific products or categories. For more information see [Customer Groups](https://support.bigcommerce.com/s/article/Customer-Groups).

**Note**
<br>
The Customer Groups feature is only available on certain plans.

## Customer Passwords
Password validation is only available on V2 Customers API. Validation will return a true or false. The V3 Customers API can reset a customers password or input a new password. 

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
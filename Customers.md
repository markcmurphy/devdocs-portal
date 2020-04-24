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
- [Differences Between V2 and V3](#differences-between-v2-and-v3-customers-api)
- [Related](#related)

</div>

</br>

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
* Customer Attribute Values
* Customer Form Field Values
* Customer Consent

## Customers

### What is a Customer?

A Customer is a shopper who has created a store account. Customer data consists of such parameters as name, email, and addresses and is stored as a customer record.

For V2 *Customers* endpoint operations, see [Customers V2](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customers/).

For V3 *Customers* endpoint operations, see [Customers V3](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customers/).

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

## Customer Addresses

Customer Addresses refers to the mailing address and the phone number associated with a Customer Account. Customers may have multiple addresses stored against them.

For *V2 Customer Addresses* endpoint operations, see [Customer Addresses V2](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customer-addresses).

For *V3 Customer Addresses* endpoint operations, see [Customer Addresses V3](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customer-addresses).

## Customer Attributes
Customer Attributes are name-value pairs associated with a Customer. For example, the name can be "Shoe Size" and the value can be 10.

Customer Attributes are created independently of the customer and are then added to the customer programmatically. 

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
### Note
> Multiple name-value pairs are allowed per customer. Each customer can have up to 100 name-value pairs.

</div>
</div>
</div>

</br>

For *V3 Customer Attributes* endpoint operations, see [Customer Attributes](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customer-attributes).

## Customer Attribute Values

Customer Attribute Values is used to access and edit the `value` property of an attribute on a Customer.   

For *V3 Customer Attribute Values* endpoint operations, see [Customer Attribute Values V3](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customer-attribute-values).

## Customer Form Field Values

Customer Form Field Values is used to access and edit customer signup and address values filled out by a customer at checkout. For example, a Wholesaler ID (a signup field) and Special Delivery Instructions (an address field). 

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
### Note
> Creating form fields is done from the Control Panel.

</div>
</div>
</div>

</br>

To learn more about adding and editing fields from the Control Panel, see [Editing Form Fields](https://support.bigcommerce.com/s/article/Editing-Form-Fields).

For *V3 Customer Form Field Values* endpoint operations, see [Customer Form Fields](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api/customer-form-fields).

## Customer Consent

Customer Consent allows merchants to access and manage customer's consent to use cookies and other technologies while shopping on a storefront. 

To learn more about requesting consent from the Control Panel, see [Security & Privacy Settings](https://support.bigcommerce.com/s/article/Store-Settings#security).

For *V3 Customer Consent* endpoint operations, see [Customer Consent](https://developer.bigcommerce.com/api-reference/store-management/customers-v3/customer-consent).

## Customer Groups

Customer Groups allows you to organize your customers, provide targeted discounts, and restrict access to specific products or categories.

<div class="HubBlock--callout">
<div class="CalloutBlock--">
<div class="HubBlock-content">
    
### Note
> The Customer Groups feature is not available on the Standard plan.

</div>
</div>
</div>

</br>

For *V2 Customer Groups* endpoint operations, see [Customer Groups](https://developer.bigcommerce.com/api-reference/store-management/customers-v2/customer-groups).

## Customer Passwords

Customer Passwords is used to validate customer passwords. It returns a true/false response indicating if the provided password matches the customer's current password. 

For *V2 Customer Passwords* endpoint operation, see [Validate a Password](https://developer.bigcommerce.com/api-reference/store-management/customers-v2/customer-passwords/validatecustomerpassword).

## Differences Between V2 and V3 Customers APIs

### Making Requests

The V3 Customers API reduces the calls needed to create and update customers. For example, you can create customer attributes and addresses in one step, allowing batch creation of multiple customers and their subresources in a single API call.

**Create a Customer**

Single Customer on V3
- `/customers`

Single Customer on V2
* `/customers/{customer_id}`
* `/customers/{customer_id}/addresses`

### Queries

With the V3 Customers API, queries become a powerful tool. Instead of using different endpoints to get customer subresources, there is one GET endpoint per resource with filters to refine the request. 

Get Customer Address by name and company on V3
`/customers/addresses?company:in=bigcommerce,commongood&customer_id:in1,2,3`

Get Customer Address by name and company on V2
`/customers/{customer_id}/addresses/{customer_address_id}`

### Upsert

Upsert is used for Customer Attributes and Form Field Values. Upsert looks for a match to the existing record and, if found, makes an update. If a match is not found, it creates a new record.

### Authentication Object

The V3 Customers API provides two ways to manage customer passwords.
 
- A new password can be set under `authentication > new password` in a PUT or POST request. 
- To have customers reset the password, change `force_password_reset` to `true` under `authentication > new password` in a PUT or POST request.

## Related

### APIs
- [Customer Login API](https://developer.bigcommerce.com/api-docs/customers/customer-login-api)
- [V2 Customers API](https://developer.bigcommerce.com/api-reference/store-management/customers-v2)
- [V3 Customers API](https://developer.bigcommerce.com/api-reference/store-management/customers-v3)
- [Subscribers API](https://developer.bigcommerce.com/api-reference/customer-subscribers/subscribers-api)

### Webhooks
- [Customers](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_customer)

### Articles
- [Editing Form Fields](https://support.bigcommerce.com/s/article/Editing-Form-Fields)  (Knowledge Base)
- [Checkout Settings](https://support.bigcommerce.com/s/article/Checkout-Settings#checkout-settings) (Knowledge Base)
- [Customer Groups](https://support.bigcommerce.com/s/article/Customer-Groups) (Knowledge Base)
- [Security & Privacy Settings](https://support.bigcommerce.com/s/article/Store-Settings#security) (Knowledge Base)
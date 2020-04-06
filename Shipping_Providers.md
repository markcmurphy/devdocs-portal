# Shipping Providers

<div class="otp" id="no-index">

### On this Page	
- [Shipping Providers](#shipping-providers)
- [Checkout Connection Options](#checkout-connection-options)
- [Rate](#rate)
- [Resources](#resources)
- [Related Articles](#related-articles)


</div>

## Shipping Providers

Shipping service providers wishing to offer shipping services and rates to BigCommerce merchants and shoppers can implement BigCommerce Shipping Provider endpoints. Once the service is implemented and accepted into BigCommerce’s shipping Carrier Registry, merchants will have access to enable and configure the service through their BigCommerce control panel. Once enabled on a store, BigCommerce will automatically retrieve the service options and rates via the provider’s endpoints and display them to merchants in the store’s control panel and to shoppers on the storefront.

Shipping Provider endpoints can also be used by merchants to retrieve rates from custom shipping tables or an in-house shipping rate calculation service.

Some use cases for the Shipping Provider API are:

* A drop-shipper that requires their own rates
* A merchant that already has a shipping table
* Third-party logistics
* Create a combination of in store pickup and shipping options for shoppers

## Checkout Connection Options
The payload sent to a Shipping Provider to check that the store is connected to this provider. Each Shipping Provider will have different configurations for the payload.

## Rate
Payload sent off to a Shipping Provider in order to get quotes.



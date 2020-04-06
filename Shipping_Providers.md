# Shipping Providers

<div class="otp" id="no-index">

### On this Page	
- [Shipping Providers](#shipping-providers)
- [Checkout Connection Options](#checkout-connection-options)
- [Rate](#rate)
- [Definitions](#definitions)
- [Related Endpoints](#related-endpoints)
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

**Prerequisites**
Required OAuth scopes: `Information` and `Settings`

## Checkout Connection Options
The payload sent to a Shipping Provider to check that the store is connected to this provider. Each Shipping Provider will have different configurations for the payload.

## Rate
Payload sent off to a Shipping Provider in order to get quotes.

## Definitions

| Name | Description |
| -- | -- |
| Configuration Fields | The fields the merchant will see in the control panel. Merchants can navigate to the Shipping Manager and enable, configure and disable the carrier for any defined zone. They will also be able to activate the app using the Carrier Connection API. Then use the Shipping Zones API and Shipping Methods API to configure the app from there. |
| Quote URL | A URL for a resource of the shipping carrier that accepts quote requests and responds with shipping quotes. For more on the Quote URL see typical app workflow below.|
| Single Carrier vs Multi Carrier | A single carrier app will offer only one shipping provider. A multi carrier app will aggregate multiple shipping carriers in one app.|
| Countries Available | A list of countries where the shipping carrier can be used. The default behavior is that the carrier is available for every shipping origin. In most cases this list should be as broad as possible. For example, if your carrier operates worldwide, make it available worldwide. The countries can be limited further than what the shipping carrier has provided. If the service is worldwide, then leave this field blank to specify that it is worldwide. This is an optional step. |
| Shipping Carrier |  A shipping carrier is what is built to provide quotes to BigCommerce. If a shipping carrier uses more than one shipping provider then it becomes a multi carrier aggregator. A carrier includes a name, description and a logo. |
| Multi-Carrier Aggregator | A shipping solution that provides shipping quotes for multiple carriers.|
| Check Connection Options URL | A URL for a shipping carrier resource that accepts check requests containing the connection options provided by a user when enabling the carrier and indicates whether or not those settings are valid. This is an optional step. |
| Shipping Quote | An estimation of cost to ship a set of items from an origin to a destination. |
| Shipping Zone | Describes a set of destination addresses and the applicable shipping settings, such as handling fees and available shipping methods.|
| Shipping Origin | The location from which goods are shipped. This determines which shipping carriers are available for the merchant to configure in the control panel. |


## Related Endpoints
- [Shipping Provider](/api-reference/store-management/shipping-provider-api)
- [Shipping Zones](/api-reference/store-management/shipping-api/shipping-zones)
- [Shipping Methods](/api-reference/store-management/shipping-api/shipping-method)
- [Shipping Carriers](/api-reference/store-management/shipping-api/shipping-carrier)

## Related Articles
- [App Store Approval Requirements](https://developer.bigcommerce.com/api-docs/partner/app-store-approval-requirements)



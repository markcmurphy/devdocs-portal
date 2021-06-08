# Developers Guide to Headless Commerce

<div class="otp" id="no-index">

### On this page
- [Ways to implement headless](#ways-to-implement-headless)
- [Storefront channels](#storefront-channels)
- [Multisite](#multisite)
- [Catalog Management](#catalog-management)
- [Cart management](#cart-management)
- [Checkout management](#checkout-management)
- [Customer login](#customer-login)
- [Sample integration](#sample-integration)
- [PCI compliance](#pci-compliance)
- [Sample API workflows](#sample-api-workflows)
- [Related resources](#related-resources)

</div>

This article provides a high level guide to using BigCommerce to power headless storefronts; we'll assume you're already familiar with headless commerce as a concept; if you're not, check out our whitepaper, [A New Era of Ecommerce: Headless Commerce](https://www.bigcommerce.com/new-era-headless-caas/) or the Help Center's [Headless Commerce Guide](https://support.bigcommerce.com/s/article/The-Headless-Approach).

## Ways to implement headless

Which headless approach fits your business requirements?

* [I want to use BigCommerce headlessly with little or no coding](#pre-built-solutions).
* [I want to build a custom solution, but I don't want to code it from scratch](#starter-apps).
* [I want to extend an existing solution or build one from scratch](#custom-solutions).

### Pre-built solutions

Want to build a headless storefront powered by a BigCommerce back-end, but don't want to write a bunch of code? Use one of the pre-built headless storefront solutions below.

|  Solution | Method of Integration | Platform | Type |
| --- | --- | --- | --- |
| [BigCommerce for Wordpress](https://wordpress.org/plugins/bigcommerce/) | WordPress Plugin | WordPress | CMS |
| [BigCommerce for Drupal](https://www.drupal.org/project/bigcommerce) | Drupal Module | Drupal | CMS |
| [Bloomreach](https://www.bigcommerce.com/apps/bloomreach/) | BigCommerce App | Bloomreach | CMS / DXP |
| [DEITY Falcon](https://www.bigcommerce.com/apps/deity-falcon-pwa-storefront/) | BigCommerce App | DEITY Faclon | PWA |
| [Next.js Commerce](https://nextjs.org/commerce) | BigCommerce App | Next/Vercel | Web App |
| [Sitrecore Extend](https://www.bigcommerce.com/apps/sitecore-extend/) | BigCommerce App | Sitecore | CMS |

[See more headless solutions and tools](https://developer.bigcommerce.com/tools-resources).

### Starter apps

Need code up a custom storefront but don't want to start from scratch? Kick-start your development with one of the following starter apps.

|  Starter | Stack |
| --- | --- |
| [gatsby-bigcommerce-netlify-cms-starter](https://github.com/bigcommerce/gatsby-bigcommerce-netlify-cms-starter) | Node / React / Gatsby / Netlify |
| [bc-nuxt-vue-starter](https://github.com/bigcommerce/bc-nuxt-vue-starter) | Node / Vue / Nuxt |
| [acf_bc](https://github.com/thirdandgrove/acf_bc) |PHP / ACF / Drupal |

[See more headless starter apps and tools](https://developer.bigcommerce.com/tools-resources).

### Custom solutions

Need to build a custom solution from scratch? BigCommerce has APIs, SDKs, and toolkits to help you do whatever you need, headlessly.

* [Create storefront channels with the Channels API](https://developer.bigcommerce.com/api-docs/channels/quick-start).
* [Manage sites and routes for headless storefronts with the sites and routes API](https://developer.bigcommerce.com/api-reference/store-management/sites).
* [Manage 301 redirects for one or more storefronts with Redirects V3 API](https://developer.bigcommerce.com/api-reference/store-management/redirects)
* [Create storefront specific product listings with the Channels API](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api).
* [Query storefront data with GraphQL](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview).
* [Use customer impersonation tokens to query data specific to the shopper](https://developer.bigcommerce.com/api-docs/storefront/graphql/graphql-storefront-api-overview#customer-impersonation-tokens).
* [Create carts with the Server-to-Server Carts API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api).
* [Fetch and display abandoned cart information using the Abandoned Carts API](https://developer.bigcommerce.com/api-reference/cart-checkout/s2s-abandoned-carts).
* [Create and manage shopper wishlists with the Wislists API](https://developer.bigcommerce.com/api-reference/store-management/wishlists)
* [Manage product data with the Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api).
* [Manage orders with Orders V2 and V3 APIs](https://developer.bigcommerce.com/api-docs/store-management/orders).
* [Use webhooks to get notified when specific events occur in BigCommerce](https://developer.bigcommerce.com/api-docs/store-management/webhooks/overview).


## Sample integration

In the diagram below, the Storefront is any location the products are being rendered and where the shopper browses for products. With headless the storefront can be a CMS or an app. The Application is making API calls to BigCommerce in order to perform certain actions and return data either to display to the shopper or pass it along to another system. BigCommerce is creating the order and processing payments so you don’t need to worry about building the infrastructure.

![Sample Headless Integration](https://storage.googleapis.com/bigcommerce-production-dev-center/images/developers-guide-to-headless-01.png "Sample Headless Integration")

|Entity|Description|
|-|-|
|**Storefront**|The front end presentation layer where a shopper interacts with products. In a headless architecture, the storefront might be a CMS, native mobile app, kiosk, static site, or any other front end solution you can imagine. The BigCommerce WordPress plugin is built using an existing CMS and injecting a stores catalog. Any CMS that accepts custom integrations can be used. Another option is to build a storefront from scratch using a framework such as [Gatsby](https://www.bigcommerce.com/blog/flexible-headless-commerce-solutions/#overview-of-bigcommerce-for-react-gatsby).|
|**Application**|Solution built by developer to control the requests and responses from the BigCommerce APIs. In addition to handling essential ecommerce tasks like requesting product information or sending the request to process a payment, the application layer can also handle logic for custom functionality, like presenting discount codes based on a shopper's history or pre filling details on the checkout page. |
|**BigCommerce**|BigCommerce will respond to the application with the requested data to power the backend ecommerce functionality. It can handle processing payments, storing customer data, retrieving the catalog and order information.|

### Managing access to your Stencil site
Once you transition to a headless setup and are no longer using your Stencil storefront, make sure to redirect shoppers to your new frontend by changing your custom domain's [nameservers](https://support.bigcommerce.com/s/article/Changing-Domains#nameservers). Also, make sure that your unused Stencil storefront is inaccessible to both search engines and shoppers. To prevent search engines from crawling and indexing your Stencil storefront, edit your robots.txt file to disallow all [robots](https://support.bigcommerce.com/s/article/Understanding-the-Robots-txt-File). To prevent shoppers from accessing your Stencil storefront's permanent URL, [Set Store as Down for Maintenance](https://support.bigcommerce.com/s/article/Maintenance-Mode) with a custom message directing shoppers to your new frontend. 



## Sample API workflows



## Resources

### Articles
- [Customers Overview](https://developer.bigcommerce.com/api-docs/customers/customers-subscribers-overview)
- [Customer Login API](https://developer.bigcommerce.com/api-docs/customers/customer-login-api)
- [Launching your store](https://support.bigcommerce.com/s/article/Launching-Your-Store)
- [PCI Compliance](https://support.bigcommerce.com/s/article/PCI-Compliance)
- [Multisite Ecommerce with WordPress and BigCommerce](https://medium.com/bigcommerce-developer-blog/multi-site-ecommerce-with-wordpress-and-bigcommerce-40dee194f8a)
- [Matter Makes Waves with a Headless Build using BigCommerce for WordPress](https://medium.com/bigcommerce-developer-blog/matter-makes-waves-with-a-headless-build-using-bigcommerce-for-wordpress-a572bad4bdf8)
- [New Era in Headless CaaS](https://www.bigcommerce.com/new-era-headless-caas/)
- [BigCommerce Doubles Down on Headless Commerce with BloomReach, Sitecore, Adobe Experience Manager, and More](https://www.bigcommerce.com/blog/flexible-headless-commerce-solutions/)
- [Merchants Classification Levels Visa](https://usa.visa.com/support/small-business/security-compliance.html#3)
- [Merchants Classification Levels Mastercard](https://www.mastercard.us/en-us/merchants/safety-security/security-recommendations/merchants-need-to-know.html)
- [Self Assessment Questionnaire (SAQ) Types and Identifying which SAQ is for you](https://www.pcisecuritystandards.org/documents/SAQ-InstrGuidelines-v3_2_1.pdf?agreement=true&time=1562173376464)
- [Maintaining Payment Security](https://www.pcisecuritystandards.org/pci_security/maintaining_payment_security)

### Endpoints
- [Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api)
- [Server to Server Checkout API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-checkout-api)
- [Server to Server Cart API](https://developer.bigcommerce.com/api-reference/cart-checkout/server-server-cart-api)
- [Orders API](https://developer.bigcommerce.com/api-reference/orders/orders-api)
- [Payments API](https://developer.bigcommerce.com/api-reference/payments)
- [Customers API](https://developer.bigcommerce.com/api-reference/customer-subscribers/v3-customers-api)
- [Validate Customer Password](https://developer.bigcommerce.com/api-reference/customer-subscribers/customers-api/customer-passwords/validatecustomerpassword)

### Tools
- [Checkout SDK](https://github.com/bigcommerce/checkout-sdk-js)
- [WordPress Plugin](https://wordpress.org/plugins/bigcommerce/)
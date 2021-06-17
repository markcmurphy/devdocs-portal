# PCI Compliance

<div class="otp" id="no-index">

### On this page	
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

This section covers the Payment Card Industry Data Security Standard (PCI DSS) compliance and your responsibilities as a third-party developer. 

BigCommerce is a PCI DSS compliant service provider and certifies [all requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/standards_overview) annually including as a shared hosting provider. The BigCommerce [PCI DSS Attestation of Compliance (AOC)](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf) describes of the technology stack certified annually. Merchants can use BigCommerce's [PCI DSS AOC](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf) to satisfy the compliance requirements for the part that outlines its responsibilities.

BigCommerce offers different avenues and channels for integration depending on the business needs. As a third-party developer, it is your responsibility to program the storefronts and recurring billing apps in a PCI compliant manner. You will also need to maintain a PCI compliance certification for third-party service providers certified by an external Qualified Security Assessor (QSA). For more information on processing payments and PCI compliance, see [PCI compliance (Payments API)](https://developer.bigcommerce.com/api-docs/store-management/payment-processing#pci-compliance). BigCommerce is only responsible for maintaining secure handling of credit cards while the payment is en route from payment request to payment processors.

## Responsibility matrix

| |BigCommerce Responsibility |Merchant Responsibility |
|--|--|--|
| BigCommerce as a storefront and backend | Responsible for all [PCI DSS requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/maintaining_payment_security) of the product to the point that it has control of merchants stores. | Responsible for ensuring that all modifications that result in external calls to, or integrations with outside parties are done in a PCI DSS compliant manner. |
||| Responsible for ensuring all design modifications are done in a PCI DSS compliant manner.|
||| Responsible for ensuring that all service providers it uses are compliant with PCI DSS.|
| BigCommerce as a backend | Responsible for all PCI DSS requirements from the point at which cardholder data is handed to a BigCommerce controlled interface (see [BigCommerce Attestation of PCI DSS 2019-2020](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf)). | Responsible for the PCI DSS compliance of its storefront plus all of the above. |
| Checkout and Payments SDK | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |
| Checkout and Payments API | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |  Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

> ### Note
> 1. The way your business consumes the SDKs (either BigCommerce as a storefront and backend or BigCommerce as a backend) determines BigCommerce's responsibilities. It is possible to use multiple BigCommerce's technology stacks at the same time. Your PCI DSS compliance responsibilities will be a combination of each stack consumed.

</div>
</div>
</div>

<div class="HubBlock--callout">
<div class="CalloutBlock--warning">
<div class="HubBlock-content">

> ### PCI compliance
> If your application handles credit card data, you will need to be PCI compliant. SAQs (self-assessment questionnaires) can be submitted to <a href="mailto:compliance@bigcommerce.com">compliance@bigcommerce.com</a>.

</div>
</div>
</div>

## Next Steps
* [Learn more about {{TOPIC}}]().

## Resources
* [Payments API](https://developer.bigcommerce.com/api-docs/store-management/payment-processing) 
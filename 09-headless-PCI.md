# PCI Compliance

<div class="otp" id="no-index">

### On this Page	
- [Section1](#section1)
- [Section2](#section2)
- [Section3](#section3)
- [Section1](#section4)
- [Section2](#section5)
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

BigCommerce offers different avenues or channels for integration, depending on your business needs. The ultimate responsibility of PCI compliance lies with you and takes into consideration the architecture of your e-commerce store and multiple channels of integrations.
BigCommerce is a PCI DSS compliant service provider and certifies annually [all requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/standards_overview) including as a shared hosting provider.

The BigCommerce [PCI DSS attestation of compliance (AOC)](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf) outlines the description of the technology stack certified annually.

Merchants can use BigCommerce's [PCI DSS AOC](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf) to satisfy the compliance requirements for the part that outlines its responsibilities.

## Responsibility matrix

| |BigCommerce Responsibility |Merchant Responsibility |
|--|--|--|
| BigCommerce as a storefront and backend | Responsible for all [PCI DSS requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/maintaining_payment_security) of the product to the point that it has control of Merchants stores. | Responsible for ensuring that all modifications that result in external calls to, or integrations with outside parties are done in a PCI DSS compliant manner. |
||| Responsible for ensuring all design modifications are done in a PCI DSS compliant manner.|
||| Responsible for ensuring that all service providers it uses are compliant with PCI DSS.|
| BigCommerce as a backend for example [headless integrations](https://developer.bigcommerce.com/api-docs/developers-guide-headless) or the [BigCommerce WordPress Plugin](https://wordpress.org/plugins/bigcommerce/). | Responsible for all PCI DSS requirements from the point at which cardholder data is handed to a BigCommerce controlled interface (see [BigCommerce Attestation of PCI DSS 2019-2020](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf)). | Responsible for the PCI DSS compliance of its storefront plus all of the above. |
| Checkout and Payments SDK | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |
| Checkout and Payments API | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |  Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup> |

<div class="HubBlock--callout">
<div class="CalloutBlock--info">
<div class="HubBlock-content">

> ### Note
> 1. The way your business consumes the SDKs (either BigCommerce as a storefront and backend or BigCommerce as a backend ) determines BigCommerce's  responsibilities; It is possible to use one more of BigCommerce's technology stack at the same time. Your PCI DSS compliance responsibilities will be a combination of each stack consumed.

</div>
</div>
</div>

<div class="HubBlock--callout">
<div class="CalloutBlock--warning">
<div class="HubBlock-content">

> If your application handles credit card data, it must be PCI Compliant. self-assessment questionnaires can be submitted to <a href="mailto:compliance@bigcommerce.com">compliance@bigcommerce.com</a>.

</div>
</div>
</div>

## Next Steps
* [Learn more about {{TOPIC}}]().

## Resources
* [Link]() 
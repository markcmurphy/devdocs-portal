# PCI Compliance

<div class="otp" id="no-index">

### On this page	
- [What is PCI?](#what-is-pci)
- [Who is responsible?](#who-is-responsible)
- [Next Steps](#next-steps)
- [Resources](#resources)

</div>

This section covers the Payment Card Industry Data Security Standard compliance and your responsibilities as a third-party developer. 

## What is PCI?

The Payment Card Industry Data Security Standard (PCI DSS) is a set of requirements designed to ensure that all companies that process, store, or transmit credit card information maintain a secure environment. For an in-depth guide to what PCI DSS is, how to achieve it for your business, and a compliance checklist, see [Everything You Need to Know About Achieving PCI Compliance](https://www.bigcommerce.com/blog/pci-compliance/).

## Who is responsible?

BigCommerce is a PCI DSS compliant service provider and certifies annually [all requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/standards_overview) including as a shared hosting provider. BigCommerce's [PCI DSS Attestation of Compliance (AOC)](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf) describes the technology stack certified annually. Merchants can use BigCommerce's PCI DSS AOC to satisfy the compliance requirements for the part that outlines its responsibilities. To learn more about demonstrating proof of PCI compliance, see [PCI Compliance](https://support.bigcommerce.com/s/article/PCI-Compliance#how).

BigCommerce offers different avenues and channels for integration depending on your business needs. It is only responsible for maintaining secure handling of credit cards while the payment is en route from payment request to payment processors. As a third-party developer, it is your responsibility to program the storefronts and recurring billing apps in a PCI compliant manner. You will need to maintain a PCI compliance certification for third-party service providers certified by an external Qualified Security Assessor (QSA). For information on processing payments and PCI compliance, see [PCI compliance (Payments API)](https://developer.bigcommerce.com/api-docs/store-management/payment-processing#pci-compliance). 

The following table outlines PCI compliance responsibilities based on the type of integration.

### Responsibility matrix

| |BigCommerce Responsibility |Merchant Responsibility |
|--|--|--|
| BigCommerce as a storefront and backend | Responsible for all [PCI DSS requirements (1-12)](https://www.pcisecuritystandards.org/pci_security/maintaining_payment_security) of the product to the point that it has control of merchants stores. | Responsible for ensuring that all modifications that result in external calls to, or integrations with outside parties are done in a PCI DSS compliant manner. |
||| Responsible for ensuring all design modifications are done in a PCI DSS compliant manner.|
||| Responsible for ensuring that all service providers it uses are compliant with PCI DSS.|
| BigCommerce as a backend. For example, headless integrations or the [BigCommerce WordPress Plugin](https://wordpress.org/plugins/bigcommerce/) | Responsible for all PCI DSS requirements from the point at which cardholder data is handed to a BigCommerce controlled interface (see [BigCommerce Attestation of PCI DSS 2019-2020](https://support.mybigcommerce.com/content/dojo/BigCommerce_PCI_DSS_v3.2.1_AOC_2019_Service_Provider.pdf)). | Responsible for the PCI DSS compliance of its storefront plus all of the above. |
| Checkout and Payments SDK | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup>. | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup>. |
| Checkout and Payments API | Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup>. |  Responsible for the PCI DSS compliance requirements applicable stated in BigCommerce as a storefront or BigCommerce as a backend<sup>1</sup>. |

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
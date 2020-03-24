## Products
Products are the primary catalog entity, and the primary function of the eCommerce platform is to sell products on the storefront, and other channels.

Products can be physical or digital:
* Physical - exist in a physical form, have a weight, and are sold by merchants with intent to ship to customers.
* Digital - Non-physical products including downloadable files such as computer software, ebooks, music, images, and other media; and services such as haircuts, consulting, or lawn care.

## Product Bulk Pricing Rules

To encourage shoppers to purchase more and in higher quantities, merchants will often offer quantity discounts on certain products, also known as bulk pricing. Bulk pricing involves offering a particular item or group of items at a lower price based on the number ordered. This is particularly useful to wholesalers and merchants who sell items that are typically bought in bulk.

You can offer bulk pricing for both individual products using Bulk Pricing Rules, and for whole categories of products (including multiple categories) using Automatic Promotions.

## Product Complex Rules

Complex rules allow merchants to set up conditions and actions based on shopper option selections on the storefront. You can use them to vary the following based on option selections made by the shopper:
* Price
* Weight
* Image
* Purchasability

Adjustments made by complex rules are displayed to shoppers in real-time on the storefront.

For the majority of merchant use cases, best practice will be to either assign values (such as a price) directly to a variant or use adjusters on the modifier option itself. However complex rules exist for rare cases where a rule condition is too complex to express in those forms easily.

Use complex rules when an adjustment should be triggered by:

* The selection of values across multiple modifier options
* The combination of a particular variant/SKU and a modifier option value.

### Complex Rules Example:

| If the product is | Variant Option | Variant |Modifier | Complex Rule |
| -- | -- | -- | -- | -- |
| T-Shirt | Blue<br>-<br> Small<br> Medium<br> Large| SM-BLU<br> SM-MED <br> SM-LARG| Checkbox<br>Donate to Charity| Checkox<br> Donate to Charity.<br> Add $5
| Backpack | Black<br>Yellow<br>-<br>2L <br> 3L<br> 8L |BLACK-2L<br>BLACK-3L<br>BLACK 8L<br>-<br>YELLOW-2L<br>YELLOW-3L<br>YELLOW-8L| Text Field<br> Add Embroidery| N/A|


## Product Custom Fields

Custom fields allow you to specify additional product information that will appear on the product page, such as a book's ISBN, a DVD's release date, or a product's material. The location of these fields on the product page may differ depending on your theme.

Custom fields will appear automatically in the product's details if they are defined on the product. A product can have a maximum of 200 custom fields, and they can be created via [CSV import](https://support.bigcommerce.com/s/article/Importing-Exporting-Products?) or through the [Catalog API](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/product-custom-fields/createcustomfield).

> **Note** 
> * Custom field values are limited to 250 characters
> * See Custom Fields in the BigCommerce Help Center for additional information on custom fields and their use-cases

## Product Images

## Product Metafields

## Product Reviews

## Product Videos

Videos hosted on YouTube can be added as product videos. 
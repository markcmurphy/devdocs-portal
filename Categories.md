# Title

<div class="otp" id="no-index">

### On this Page	
- [Categories](#categories)
- [Category Images](#category-images)
- [Category Metafields](#category-metafields)
	
</div>
<br>

The Catalog API manages products, brnds, and categories for a store. This section focuses on categories.

## Categories

Create and manage categories.

Categories are a hierarchy of products available on the store, presented in a tree structure. A store’s category structure determines the primary menu structure of most storefront themes, which are directly tied to it.

All products must be associated with at least one Category, although a Category does not need to contain any products. Unlike some e-commerce platforms, products on BigCommerce can be associated with more than one Category.

A product associated with categories does not currently have any priority or weighted order (there’s no “primary category”), which can make it difficult to integrate with some external systems which might wish to use a product’s categories to map to a category structure in that external system.

Categoty Tree endpoint returns a simple view of the parent - child relationship of all categories in the store. This endpoint can be used to fetch categories when building a custom navigation for a store. 

|Resource / Endpoint|Description|
|-|-|
|[`Get All Categories`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/getcategories)|Returns a list of Categories|
|[`Create a Category`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/createcategory)|Creates a Category|
|[`Delete Categories`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/deletecategories)|Deletes all Category objects|
|[`Get a Category`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/getcategorybyid)|Returns a single Category|
|[`Update a Category`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/updatecategory)|Updates a Category|
|[`Delete a Category`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/deletecategorybyid)|Deletes a Category|
|[`Get Category Tree`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/getcategorytree)|Returns a view of the parent-child relationship of all categories|

## Category Images

Create and manage category images.

**Notes**

* Only one image can be created at a time. 
* Limit image size to 1MB. 
* To update a Category Image, use [Update a Category](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category/updatecategory) and an `image_url`.

|Resource / Endpoint|Description|
|-|-|
|[`Create a Category Image`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-images/createcategoryimage)|Creates a Category Image|
|[`Delete a Category Image`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-images/deletecategoryimage)|Deletes a Category Image|

## Category Metafields

Create and manage category metafields. 

|Resource / Endpoint|Description|
|-|-|
|[`Get All Category Metafields`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-metafields/getcategorymetafieldsbycategoryid)|Returns a list of Metafields on a Category|
|[`Create a Category Metafield`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-metafields/createcategorymetafield)|Creates a Cateory Metafield|
|[`Get a Category Metafield`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-metafields/getcategorymetafieldbycategoryid)|Returns a single Category Metafield|
|[`Update a Category Metafield`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-metafields/updatecategorymetafield)|Updates a Category Metafield|
|[`Delete a Category Metafield`](https://developer.bigcommerce.com/api-reference/catalog/catalog-api/category-metafields/deletecategorymetafieldbyid)|Deletes a Category Metafield|

### Resources

[Webhook Events](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_category)

[Theme Docs: Category](https://developer.bigcommerce.com/stencil-docs/reference-docs/other-objects-and-properties-overview#category)

[Help Center: Product Categories](https://support.bigcommerce.com/s/article/Product-Categories)
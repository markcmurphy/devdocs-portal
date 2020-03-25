# Title

<div class="otp" id="no-index">

### On this Page	
- [Categories](#categories)
- [Category Images](#category-images)
- [Category Metafields](#category-metafields)

</div>

The Catalog API manages products, brnds, and categories for a store. This section focuses on categories.

## Categories

Create and manage categories.

Categories are a hierarchy of products available on the store, presented in a tree structure. A store’s category structure determines the primary menu structure of most storefront themes, which are directly tied to it.

All products must be associated with at least one Category, although a Category does not need to contain any products. Unlike some e-commerce platforms, products on BigCommerce can be associated with more than one Category.

A product associated with categories does not currently have any priority or weighted order (there’s no “primary category”), which can make it difficult to integrate with some external systems which might wish to use a product’s categories to map to a category structure in that external system.

Categoty Tree endpoint returns a simple view of the parent - child relationship of all categories in the store. This endpoint can be used to fetch categories when building a custom navigation for a store. 

## Category Images

Create and manage category images.

## Category Metafields

Create and manage category metafields. 

### Resources

[Webhook Events](https://developer.bigcommerce.com/api-docs/getting-started/webhooks/webhook-events#webhook-events_category)


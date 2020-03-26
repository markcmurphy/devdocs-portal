## Widgets

Widgets are the units of content to be placed on specific pages in a Stencil theme. Each widget is comprised of a widget configuration and a widget template. 

>**Note**
>
>There is a limit of 1000 widgets per store.

The Widgets API allows developers to programmatically associate content with regions on a BigCommerce storefront. The content can consist of HTML, CSS, and JavaScript. The API supports configuration via Handlebars variables. It can support many types of content such as YouTube Videos, image sliders, and chat apps.

Some benefits are:
* Inject modular, reusable blocks of content inside new and existing store pages
* Build tools that allow non-technical users to control content without editing theme files
* Target specific products, categories or brands with widgets

## Widgets Placements
Placements determine the Region where the Widget is placed and in what order. The order of the placement is controlled by the `sort_order` when creating the placement. A placement must be created in order to use a Widget on the storefront.

Placements can be used with `sort_order` and region to determine placement in a theme.

Placements are the records to track which widget appears on which page, and in what order. Currently, placements can only exist on the following pages:
* pages/blog-post
* pages/blog
* pages/brand
* pages/brands
* pages/cart
* pages/category
* pages/home
* pages/page
* pages/product
* pages/search

>**Note**
>
>There is a limit of 75 placements per template file and 6500 total placements per store.

### Placements `entity_id`
When creating a placement, there is an option to provide an `entity_id`. This is the ID for a specific product, brand, category or page. For example, if a Widget needs to be on all product pages, leave `entity_id` blank. If the Widget should only appear on a certain product page, then assign `entity_id` the product ID.

`entity_id` can be used with the following page types:
* pages/brand
* pages/category
* pages/page
* pages/product

## Widgets Region
Regions are specific locations in the Stencil theme files where a Widget is placed. A region is added at the file level using the format `{{{region name="…"}}}`. A region can be named however you like, but it is best practice to give it a name that is descriptive of the location and function. A theme file can have as many regions as you want, with more than one widget assigned to the region and the Placement sort_order controlling how the widgets appear on the Storefront.

Most themes in the BigCommerce marketplace come with predefined regions. It is best to utilize those first. By editing the theme and adding theme regions, updates will need to be manually managed.

## Widgets Templates
Widget Templates are Handlebars-enabled HTML templates which define the Widget’s structure on a page. These templates can include conditional logic as well as looping. Widget templates can be reused to build multiple widgets.

>**Note**
>
>There is a limit of 100 total custom widget templates per store. This does not include templates pre-provided by BigCommerce.

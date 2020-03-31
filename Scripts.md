<div class="otp" id="no-index">

### On this Page	
- [Scripts](#scripts)
- [Scripts Manager API Partner Guidelines](#script-manager-partner-guidelines)

</div>

## Scripts

The BigCommerce Scripts API gives developers the ability to inject scripts into a store's template files programmatically. This means that app and integrations can insert scripts into a user’s storefront without requiring the user to manually paste a snippet of code into their control panel. There are many use cases for this powerful API, for example:
* inserting analytics scripts
* inserting single-click app scripts
* inserting live chat and support plugins
* inserting theme extensions or connector apps

## Script Manager API Partner Guidelines

With the Script Manager API, your Apps now have the ability to insert scripts into a user’s storefront without requiring the user to manually paste a snippet of code into the Control Panel. You can freely update these scripts while your App is installed, and — if desired — automatically remove scripts if your App is uninstalled.

For Apps installed on our latest theme engine, Stencil), this process is straightforward. If your App is already live, you may have requested merchants paste a code snippet in one of two sections in the control panel:

- Footer Scripts
- Web Analytics

Because our older, Blueprint-based themes do not support the Script Manager API, you’ll still need a way of providing these users with the instructions for adding necessary scripts to their storefronts, without burdening users of newer themes with unnecessary steps.

To help you transition to the Script Manager API, we’ve provided some recommended strategies to deal with these different situations. 

#### Stencil vs Blueprint

As mentioned above, BigCommerce supports two theme engines: Stencil and Blueprint. Stencil is our latest theme framework, and all new stores only have access to Stencil themes. However, older stores may still be using our legacy theme engine, Blueprint, which cannot render scripts inserted via the Script Manager API.

Because of this, you’ll need to check whether a user is running Stencil to determine if their store supports the Script Manager API. To do this, use the [Get Store Information API](https://developer.bigcommerce.com/api/v2/#store-information-reference) endpoint and check the `stencil_enabled` flag. (requires [store_v2_information_read_only scope](https://developer.bigcommerce.com/api/#oauth-scopes)).


### Installing An App on Stencil

For Apps being installed on Stencil stores, we recommend inserting your scripts immediately after receiving the POST response during the [Auth Callback flow](https://developer.bigcommerce.com/api-docs/getting-started/building-apps-bigcommerce/building-apps#installation-and-update-sequence). Add your scripts using the `Create Script` endpoint of the Script Manager API.

We recommend leaving the `auto_uninstall` flag set to true, so that your App will properly remove scripts when uninstalled. 


## Notes

- If you are injecting scripts into the Checkout, you will need to update the scope to Checkout Content. Accounts can only be created by the [store owner](https://support.bigcommerce.com/articles/Public/Store-API-Accounts/).
- Merchants will be able to see the scripts installed on the store in the Control Panel. Within the native tag manager, merchant actions will be limited to viewing a script and deleting a script.
- Scripts can be located in the header `{{head.scripts}}` or footer `{{footer.scripts}}`.
- Scripts Manager is only for Stencil themes. Blueprint store users will still need to copy and paste in code.
- The current visibility options are `storefront`, `checkout`, `all_pages` and `order_confirmation`.
- Scripts injected via the Scripts API will not render when you are developing a theme locally via Stencil CLI.
- Each app can have 10 scripts. 
- Up to five scripts can be installed in a single call. 

```js
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'GA_TRACKING_ID');
</script>
```

## Script Visibility Locations

| Scope | Visibility |
| -- | -- |
| `all_pages` | Add Wishlist </br> Blog List </br> Blog Post</br> Brand Pages </br> All Brands Page </br> Cart </br> Category </br> Checkout </br> Checkout </br> Product Compare </br> Order Confirmation </br> Page </br> Contact Form </br> Product </br> Search </br> All Wishlist </br> Wish List <br> 404 page |
| `storefront` |  Add Wishlist </br> Blog List </br> Blog Post</br> Brand Pages </br> All Brands Page </br> Cart </br> Category </br> Checkout </br> Checkout </br> Product Compare </br> Page </br> Contact Form </br> Product </br> Search </br> All Wishlist </br> Wish List <br> 404 page|
| `checkout` | Checkout | 
| `order_confirmation` | Order Confirmation | 

Scripts can not be injected to:
- giftcertificates.php
- sitemap.php
- account.php
- login.php

## Resources

- [App Installation](/api-docs/getting-started/building-apps-bigcommerce/building-apps#building-apps_installation-update-sequence)

## Related Endpoints
* [Scripts](/api-reference/content/content-scripts-api)

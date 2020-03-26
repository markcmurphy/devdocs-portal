<div class="otp" id="no-index">

### On this Page	
- [Channels](#channels)
- [Channel Listings](#channel-listings)
- [Channel Sites](#channel-sites)
- [Channel Site Routes](#channel-site-routes)

</div>
<br>

Introduction

## Channels

Create and manage product listings for multiple storefronts and sales channels. 

A channel is anywhere a merchant sells their products. This encompasses headless storefronts, marketplaces, POS systems, and marketing platforms.

|Resource / Endpoint|Description|
|-|-|
|[`Get All Channels`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channels/listchannels)|Returns a list of Channels|
|[`Create a Channel`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channels/createchannel)|Creates a Channel|
|[`Get a Channel`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channels/getchannel)|Returns a Channel|
|[`Update a Channel`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channels/updatechannel)|Updates a Channel|

## Channel Listings 

Manage catalog differences among different storefronts or marketplaces. 

Channel listings allow you to manage catalog differences among different storefronts or marketplaces.

|Resource / Endpoint|Description|
|-|-|
|[`Get Channel Listings`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-listings/listchannellistings)|Returns a list of all Channel Listings|
|[`Update Channel Listings`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-listings/updatechannellistings)|Updates a Channel Listing|
|[`Create a Channel Listing`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-listings/createchannellistings)|Creates a Channel Listing|
|[`Get a Channel Listing`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-listings/getchannellisting)|Returns a Channel Listing|

## Channel Sites

Manage sites and routing for headless storefronts. 

|Resource / Endpoint|Description|
|-|-|
|[`Get a Channel Site`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-site/get-channel-site)|Returns Site data|
|[`Update a Channel Site`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-site/put-channel-site)|Updates a Site|
|[`Create a Channel Site`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-site/postchannelsite)|Creates a Channel Site|
|[`Delete a Channel Site`](https://developer.bigcommerce.com/api-reference/cart-checkout/channels-listings-api/channel-site/deletechannelschannelidsite)|Deletes a Channel Site|

## Channel Site Routes


### Sites and Routes

Sites and routes control the paths that make up a headless storefront.

A site refers to the domain associated with a channel. 

Routes point to the URLs for key pages on the headless storefront. They define where your homepage is, where your cart page is, etc.

Sites and routes ensure links point where they’re supposed to and sales are attributed correctly. For example, a shopper’s order confirmation email should link back to Storefront A, where they placed their order, not Storefront B, which they’ve never visited. 

For more information, see [Sites and Routes API](https://developer.bigcommerce.com/api-reference/cart-checkout/sites-routes-api). 

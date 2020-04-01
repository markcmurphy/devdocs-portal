<div class="otp" id="no-index">

### On this Page	
- [Themes](#themes)
- [Resources]()
- [Related Articles](#related-articles)

</div>

## Themes
The Themes API allows for the management of Stencil themes on a store. In this API, Themes are treated as a single object (.zip file), and not as a collection of files. This API is useful for backing up/restoring themes, as well as for creating a theme publishing workflow.

As themes must be processed once uploaded or before being downloaded, this API provides job IDs for long-running processing jobs, and a jobs endpoint which you may poll for updates.Before a theme may be uploaded to this API, it should be bundled using stencil-cli.

Themes downloaded from this endpoint may be edited using stencil-cli for local development.

## Actions Download
Downloads a stores Theme.

## Actions Activate
Actives a store Theme.

## Theme Jobs
The job for theme upload or download


## Resources
[Stencil Themes](https://support.bigcommerce.com/s/article/Stencil-Themes#intro1)
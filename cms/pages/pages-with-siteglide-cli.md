---
title: Pages with Siteglide CLI
slug: 0e2i-
createdAt: 2021-02-18T10:52:51.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# 💻 Pages with Siteglide CLI

When the Admin builds a Page, it adds important metadata using the YAML language.

It also includes Liquid code, hidden from Admin, which controls automatic metadata output and Secure Zones if relevant.

If you add Pages locally, you'll need to add this data.`-`

Pages must be stored within the following file path of your project: `marketplace_builder/views/pages/` and must be `.liquid` file type.

{% content-ref url="pages-and-page-templates-file-structure.md" %}
[pages-and-page-templates-file-structure.md](pages-and-page-templates-file-structure.md)
{% endcontent-ref %}

## Yaml Settings and Metadata

This is an example Page generated by Siteglide. Below, we'll list available YML parameters, and body content.

The YML section of the page is marked by triple dashes above and below. Everything below is the main body of the page, in liquid language.

YML is very strict about spaces and tabs- always use two spaces instead of a tab in YML.

If you wish to use Liquid in the redirect to line, you can make the line multiline: [https://documentation.platformos.com/use-cases/using-liquid-markup-yaml#using-liquid-markup-in-yaml](https://documentation.platformos.com/use-cases/using-liquid-markup-yaml#using-liquid-markup-in-yaml)

```yaml
---
slug: a-site-page
layout_name: templates/1
metadata:
  name: My first page
  file_type: page
  last_edit: 1550810046465
  meta_title: My site - My first page
  meta_desc: Here's some text to show in search engine
  og_title: My site - My first page
  og_desc: Here's some text to show in search engine
  og_type: article  
  twitter_type: app
  enabled: true
physical_file_path: views/pages/a-site-page.liquid
redirect_to: '/'
redirect_code: 301
searchable: true
---

<div data-gb-custom-block data-tag="include" data-0='modules/siteglide_system/constants'></div>

<!-- Page Content Here -->
```

### Parameters

*   `Slug` - This is the page URL. Must be unique - Siteglide Admin handles this when editing Pages there, but we obviously have little control over that here, so it's up to the user to maintain for now (we can add validation later). Shouldn't ever be '/', as that's reserved by homepage. If you need to set it as homepage you'll have to do via UI for now. (required)`layout_name` - Reference your Template here. Stored at -> marketplace\_builder/views/layouts/templates/1.liquid

    `metadata`

    * `name` - Page name shown in UI (required) Note: This must be a string
    * `file_type` - Set as 'page' (required)
    * `last_edit` - timestamp of last edit - shown in UI
    * `meta_title` - Used in page title
    * `meta_desc` - Used as meta description
    * `og_title` - Used in page data for sharing link
    * `og_desc` - Used in page data for sharing link
    * `og_type` - Defines page content type for sharing link
    * `twitter_type` - Defines page content type for twitter sharing link
    * `enabled` - If the page is visible on the front-end
    * `use_siteglide_js` - Set as 'false' to supress the siteglide.js file from being included in your page. Note: This will stop forms from submitting, only turn this off on pages that do not include forms. Currently this does not work for the homepage of your site
* `physical_file_path` - Files should be stored in a location relative to their slug. If your slug is /services/cleaning, then the physical\_file\_path would be views/pages/services/cleaning.liquid - **note changing this line can have unexpected results.** If you want to move a file, you can just move the file and delete this line. Re-syncing or deploying should change the physical file path automatically.
* `redirect_to` - The slug to redirect to, if it needs it. If it's homepage, you need to redirect to '/'
* `redirect_code` - Set as '301' if there's a redirect
* `searchable` - Set as 'true' so it shows in search results
* `layout` - Adds the [Page Template](broken-reference) e.g. set to 'templates/1' for the template with an ID of 1. Or to leave blank for API Endpoints, set to empty string ''.

**Body** must include the constants snippet shown in example for features like SEO and Secure Zones to work.

## Liquid Visible in CLI Only

### Constants

Constants makes certain variables available in the Page and passes others up to the Page Template e.g. SEO. It should sit at the very top of most pages.\
\
If you are confident a Page doesn't need it e.g. an API Endpoint, you can skip it to improve performance.

```liquid
{% raw %}
{% include 'modules/siteglide_system/constants' -%}
{% endraw %}

```

### Secure Zones

You can use your own Liquid to implement logic based off the logged in User's Secure Zones, but to copy the pattern Admin creates for consistency you can do this:

```liquid
{% raw %}
{% include 'secure_zones', secure_zones_string: '1' -%}
{% if context.exports.access_allowed.value == true -%}
  {% comment %}Your Page Code here!{% endcomment %}
{% else -%}
  {% include '401' -%}
{% endif -%}
{% endraw %}
```

Replace the "secure\_zones\_string" with the ID of your relevant Secure Zone from Admin.
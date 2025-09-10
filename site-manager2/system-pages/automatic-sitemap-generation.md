# Automatic Site Maps

You can output a list of pages using the following include:

```liquid
{% include 'sitemap', layout: 'xml', types: 'pages' -%}
```

*   layout - xml or html - These are set layouts for each type. html will output in

    * format.
    * types - Choose what types of content you want to show, by submitting a comma separated list from these options: `pages,webapps,modules,products,categories`

    The sitemap will only show items that are enabled, have a detail view, have a slug and are within their released/expired timeframe.\
    \
    Pages need to have `metadata.file_type` set to "page" before they will appear in either type of Sitemap. This will be automatically added to any page created in Siteglide Admin, but will need to be added manually, if desired, to pages created in Siteglide CLI.\
    \
    For pages, the displayed pages will depend also on the format:
*   XML format sitemaps will not display pages which have metadata.seo\_searchable set to false, whereas HTML format sitemaps will.\


    For best results, use this include on your sitemap.xml System Page (with the xml layout) and optionally also on your own custom Page (with the html layout).\
    \
    It is also recommended to add an absolute link to your XML sitemap in your robots.txt system page e.g.

```
Sitemap: https://www.example.com/sitemap.xml
```

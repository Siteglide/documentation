# Automatic Site Maps

You can output a list of pages using the following include:

```liquid
{% include 'sitemap', layout: 'xml', types: 'pages' -%}
```

* layout - xml or html - These are set layouts for each type. html will output in
* types - Choose what types of content you want to show, by submitting a comma separated list from these options: `pages,webapps,modules,products,categories`

The sitemap will only show items that are enabled, have a detail view, have a slug and are within their released/expired timeframe.\
\
Pages need to have `metadata.file_type` set to "page" before they will appear in either type of Sitemap. This will be automatically added to any page created in Siteglide Admin, but will need to be added manually, if desired, to pages created in Siteglide CLI. If you want to hide a page from the HTML sitemap and the Siteglide Admin, you can remove this in CLI (useful for test pages). \
\
For pages, the displayed pages will depend also on the format:

* XML format sitemaps will not display pages which have `Visible to search engines` set to false (in CLI this is metadata.seo\_searchable), whereas HTML format sitemaps will ignore this setting. It should be noted though that this setting also adds a noindex HTML tag to the page in question, so any robots crawling the HTML sitemap will still not crawl these pages.

For best results, use this include on your sitemap.xml System Page (with the xml layout) and optionally also on your own custom Page (with the html layout).\
\
It is also recommended to add an absolute link to your XML sitemap in your robots.txt system page e.g.

```
Sitemap: https://www.example.com/sitemap.xml
```

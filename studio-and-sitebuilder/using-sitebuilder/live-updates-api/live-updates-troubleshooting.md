# Live Updates Troubleshooting

1\) Live updates automatically strips out `&lt;script&gt;` tags from updated HTML, for security and performance reasons. This can cause problematic behaviour on Product List views with add to cart buttons on each item.

To solve this, you can add the following code manually on the top of the wrapper or page:

```liquid
<script>window.s_csrf_token = "{{context.authenticity_token}}";</script>
<script async src="{{ 'modules/siteglide_ecommerce/js/siteglide_ecommerce.js' | asset_url }}"></script>
```

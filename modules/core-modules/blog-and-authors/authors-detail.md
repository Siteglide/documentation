# Authors Detail

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

1. Make sure the Authors module is installed. You may also want to install the Blog module.
2. Create an Authors detail layout, or install one from the SiteBuilder module. An Authors detail layout should:
   1. Be stored in the code editor folder: layouts/modules/module\_6/`&lt;layout\_name&gt;`/detail/
   2. Contain at least a wrapper.liquid and an item.liquid file.
   3. The wrapper file should contain the code below where the dynamic single item.liquid file for the specific author should be outputted: `{%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}`
   4. The item file should contain the fields needed to display information about a specific author. You can check available data by outputting the `this` object as JSON using `{{this}}` .
   5. You may also wish to output a Blog list view, filtered so that only the current author's articles are displayed: `{% hash_assign context['params']['module_field_3_4'] = this.id %}{% include 'module', id: '3', type: 'list', layout: '<layout_name>', per_page: 12, show_pagination: 'false', use_adv_search: 'true' %}`  Make sure to replace `<layout_name>` with the name of your blog list layout. Since you're including a list view inside a detail view, the "type" parameter is mandatory here.
3. Navigate to Modules/Authors in the Admin Menu

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

4. Click the View Table button to update settings

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

5. Turn on Detail views, and select a slug, Page Template and Detail layout.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

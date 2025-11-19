# Live Updates Example - Enforcing Filters

### Introduction and Use Cases <a href="#introduction-and-use-cases" id="introduction-and-use-cases"></a>

This example is useful if you want to use [Siteglide filters](../../../webapps/layouts/searching-advanced-filtering.md) on a WebApp or Module, but don't want to give your end-user the option of altering the filters by modifying the URL.

In this example, we set the filter as if we have a WebApp 1 with a custom field (perhaps a select field) which can be filtered. Let's assume we need to only show items where the value of webapp\_field\_1\_1 is a or b, and we don't want the user to be able to change that. These variables of webapp, field and filter value you can change depending on your use-case.

### Example <a href="#example" id="example"></a>

#### Liquid in the wrapper.liquid file <a href="#liquid-in-the-wrapperliquid-file" id="liquid-in-the-wrapperliquid-file"></a>

```liquid
{% comment %} Get public key as normal {% endcomment %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model, collection: 'false', creator_id: nil %}
{% comment %} Generate unique ID for the layout, unless one has already been generated and sent in the params. The main purpose of doing this here is to help the JavaScript reliably reference the instance of the Live Update object created for this layout.{% endcomment %}
{% if params.sitebuilder_uniq_component_id %}
  {% assign sitebuilder_uniq_component_id = params.sitebuilder_uniq_component_id %}
{% else %}
  {% capture sitebuilder_uniq_component_id %}sitegurus_component_{% increment sitegurus_gen_uniq_component_id %}{% endcapture %}
{% endif %}
{% comment %} Output Layout Wrapper code. {% endcomment %}
<section data-sg-live-update-key="{{public_key}}" id="{{sitebuilder_uniq_component_id}}_table" data-sg-live-update-section="{{sitebuilder_uniq_component_id}}">
  <form class="hidden" data-sg-live-update-controls="hidden">
    <input type="hidden" name="webapp_field_1_1" value="a,b">
    <input type="hidden" name="webapp_field_1_1_match_type" value="OR">
  </form>
  {% comment %} Logic which will refuse to display any items until the correct filter is applied. {% endcomment %}
  {% if params.webapp_field_1_1 != "a,b" %}
    {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
  {% endif %}
</section>
```

Drawing your attention to the important bits: 

Items are not displayed until the correct parameters are present in the URL. Users can't simply change the URL and access different content in this case!

```
{% if params.webapp_field_1_1 != any_variable %}
  {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
{% endif %}
```

Usually, with this setup, the server won't render the items on initial page load, only on re-render, since the param will not be available on initial page load usually.

In version >= 1.6, an initial re-render will happen immediately if there are controls with initial values the layout using the filter param as soon as possible . The second hidden field allows either a OR b to match- which allows for more flexibility.&#x20;

```
<form class="hidden" data-sg-live-update-controls="hidden">   
  <input type="hidden" name="webapp_field_1_1" value="a,b">
  <input type="hidden" name="webapp_field_1_1_match_type" value="OR">
</form>
```

You can also use this method to check certain Secure Zones and compare them to filter parameters.

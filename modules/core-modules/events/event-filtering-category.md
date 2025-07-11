# Filter by Category

You can dynamically output a navigation menu of Categories which have Events assigned to them. The User can then filter the Events.

## Prerequisites

* You have Installed Events Module
* You have added at least one Category to an Event

## Introduction

This Article will show:

* How to include this Navigation Option when including the Events List
* The Default Layouts with explanation
* How to give the User Feedback on the type of results they are seeing.

## To Include this Option

Include the following liquid to dynamically get a list of available Events Categories for the User to select:

```liquid
{%- include 'modules/siteglide_system/get/get_categories'
    categories_layout: 'design_system/1/categories'
    categories_layout_type: 'list' 
-%}


```

The parameters refer to Layouts which will be used to display the Category links.

* `categories_layout` should be the path to the folder in the Events Module where your Category Navigation files are stored.
* The `category_layout_type` is the sub-folder where the wrapper and item files are stored for filtering the Events list by category e.g. `list`. The `category_layout_type` exists because some Events layouts may have a different partial layout for Categories within a Events preview, footer or sidebar.

## Default Layout Examples with Explanation

#### wrapper.liquid

```liquid
<div class="row no-gutters">
  <div class="col-12">
    <h2>Categories</h2>
    <ul>
      {%- include 'modules/siteglide_system/get/get_items'
        item_layout: 'item' 
      -%}
    </ul>
  </div>
</div>


```

#### item.liquid

```liquid
<li>
       <a
              href="{{context.headers.PATH_INFO}}?category={{this.id}}" 
              title="Category: {{this.properties.name}}"
       >
              {{this.properties.name}}
       </a>
</li>


```

The link should be the slug of your Events List view followed by `?category={{this.id}}`. Siteglide will be able to read the Category id from the URL and populate the List View on refresh. In this example we use the context object to automatically get the slug of the current Events Page.

## User Feedback - Displaying the currently applied filter

You may wish to give the User some feedback about the current filter/ search terms that are applied on the Events List. For Categories, you can use `{{context.exports}}` object to get the name of the category you are filtering by:

```liquid
{% if context.params.category %}
  {{context.exports.categories.data[context.params.category].name}} Events
{% endif %}
```

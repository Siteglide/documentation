# ℹ️ Standard List View

We'll explain how to output a List View of Events and link you to the docs on advanced Filtering and Navigation

## Introduction

The Events Module comes with a wide range of options for your List View. You can output Events as:

* A standard List
* [A Map](/modules/core-modules/events/event-list-map.md)
* [A Calendar](/modules/core-modules/events/event-list-calendar.md)

You can also use our [Navigation options](/modules/core-modules/events/get-started-event-filtering.md) with any of these views.

## Outputting a List View

You can output a List View in any Liquid File - that means:

* Pages
* Templates
* Headers
* Footers
* Layouts
* Code Snippets
* Content Sections

Basic List views will also work in workflow and auto-responder emails, but be aware that any features which depend on JavaScript or URL parameters will not be supported in this context- that includes the Map and Calendar Layouts.

Use the following Liquid Syntax to output an Events List view:

```liquid
{% raw %}
{%- include 'module'
    id: '12'
    layout: 'design_system/1/list'
    per_page: '2000'
    show_pagination: 'false'
    sub_model: 'true' 
-%}
{% endraw %}
```

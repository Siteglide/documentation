# 🔹 Filtering WebApps and Modules by Categories Using Liquid Parameters

This Article shows how to filter WebApp and Module Items using their category\_ids parameter.

## Introduction

In this set of Articles, we'll show you the Liquid syntax needed to get the most out of [Categories](https://help.siteglide.com/article/123-categories-getting-started) on the Front End.

You can use Category IDs to filter WebApp, Module or eCommerce Product Items when including a List View in the Page.

## Filtering by a Single Category or Multiple Categories

You can filter by a single Category using category\_ids:

```liquid
{% include 'module'
   id: '3'
   layout: 'default'
   per_page: '20'
   sort_type: 'properties.name'
   sort_order: 'asc'
   category_ids: '1' 
%}

```

You can filter by multiple Categories using comma-separated values in the category\_ids parameter:

```liquid
{% include 'module'
   id: '3'
   layout: 'default'
   per_page: '20'
   sort_type: 'properties.name'
   sort_order: 'asc'
   category_ids: '1,2,3' 
%}

```

## WebApps and Modules

This parameter works whether you're filtering WebApps or Modules!

#### WebApp

```liquid
{% include 'webapp'
   id: '3'
   layout: 'default'
   per_page: '20'
   sort_type: 'properties.name'
   sort_order: 'asc'
   category_ids: '1,2' 
%}

```

#### Module

```liquid
{% include 'mdoule'
   id: '3'
   layout: 'default'
   per_page: '20'
   sort_type: 'properties.name'
   sort_order: 'asc'
   category_ids: '1,2'
%}

```

#### eCommerce Products

```liquid
{%- include 'ecommerce/products'
    layout: "my_layout"
    category_ids: '1,2'
    type: 'list' 
-%}
```

## Nested Categories

If you filter by a Category which contains sub-Categories, the results will include all Items belonging to the Sub-Categories.

E.g. If you have a Products Category containing Merchandise and Music, filtering by the ID of the Products Category will return all Items belonging to Products, Merchandise and Music.

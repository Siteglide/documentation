---
description: >-
  This may also help troubleshoot issues with modules. Some frequently asked
  questions and a checklist of things to try when your webapp/module tag is not
  behaving as expected.
icon: wrench
---

# WebApp Troubleshooting

### Check your Liquid tag parameters are valid

Invalid Liquid tag parameters can cause a GraphQL error behind the scenes. While we don't expose this error message to the page (so your users don't see it) the common symptom of this problem would be no available data in your layout, or the layout not rendering at all. To test for that, try outputting in your layout:

```
{{this}}
```

If nothing appears, you might have this problem. \
\
An example of a Liquid tag with invalid parameters is this one, can you spot the issue?

```
{% include 'webapp', id: '1', item_ids: '1', per_page: '1', sort_type: 'item_ids', layout: 'widget-test' -%}
```

Answer: `item_ids` is a valid parameter name, but not a valid parameter value for  the parameter `sort_type`. To \*sort\* by the item's id, the correct value would be `sort_type: "id"` , since id is a core field shared by all webapps and modules. Other core fields include "created\_at", "updated\_at", "external\_id". Most other fields e.g. `expiry_date` , `name` or custom fields are Siteglide fields and should be prefixed by `properties` e.g. `sort_type: "properties.name"` .

### Nesting a List inside a Detail

When you include a webapp or module list, you don't normally need to specify the `type` parameter. This changes when you're nesting that list inside a detail view. That's because the inner include tag "inherits" the value from the detail layout, causing it to attempt to load a detail view itself. \
\
So you need to then specify that the type is list:

```liquid
{% include 'webapp', id: '1', layout: 'default', type: 'list' %}
```


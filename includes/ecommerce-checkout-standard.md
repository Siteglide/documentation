## What is it?

This is used to output payment fields in a checkout form.

## Where to use?

You should include this on a checkout form.

## How to use?

### Outputting 1 payment gateway option

```html
{%- include 'ecommerce/checkout_standard' -%}
```

This will output the Payment Gateway that you most recently updated in Siteglide Admin.

### Outputting multiple payment gateway options

```html
{%- include 'ecommerce/checkout_standard'
    id: '123'
    default: 'true'
-%}
```

This will output the Payment Gateway with the ID you select.
When outputting by ID, you should select which is the default option.

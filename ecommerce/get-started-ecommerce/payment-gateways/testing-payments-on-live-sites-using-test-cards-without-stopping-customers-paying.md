---
description: >-
  When on staging sites, it's easy to test payments by using the Payment
  gateway's test mode toggle, but what about on live sites? Stop using developer
  discount codes and set up a test mode.
---

# Testing Payments on Live Sites using test cards -without stopping customers paying

See [https://docs.siteglide.com/en/ecommerce/get-started-ecommerce/payment-gateways/switching-gateway](https://docs.siteglide.com/en/ecommerce/get-started-ecommerce/payment-gateways/switching-gateway) for giving the customer a choice of Gateway using JS.\
\
Follow the instructions for each payment form you want to be able to test on:\
\
1\) Check the form is using a custom layout (not default). You need to be able to modify the layout and keep changes. \
\
2\) Depending on whether your form is a basic payment form or checkout form, you should have one of these two tags:

{% code lineNumbers="true" %}
```liquid
{% include "ecommerce/basic_payment",
  amount: '500'
%}
```
{% endcode %}

{% code lineNumbers="true" %}
```liquid
{%- include 'ecommerce/checkout_standard'-%}
```
{% endcode %}

You need to add the ID parameter of the main enabled and live payment gateway on these, and the default parameter.

{% code lineNumbers="true" %}
```liquid
{% include "ecommerce/basic_payment",
  amount: '500',
  id: '1',
  default: 'true'
%}
```
{% endcode %}

{% code lineNumbers="true" %}
```liquid
{%- include 'ecommerce/checkout_standard', id: '1', default: 'true' -%}
```
{% endcode %}

\
3\) Now switch the ID to work on Liquid reading the URL parameter, with a default for the ID of your live gateway:\


{% code lineNumbers="true" %}
```liquid
{% assign payment_gateway = context.params.test | default: "1" %}
{%- include 'ecommerce/checkout_standard', id: payment_gateway , default: 'true' -%}
```
{% endcode %}

{% code lineNumbers="true" %}
```liquid
{% assign payment_gateway = context.params.test | default: "1" %}
{% include "ecommerce/basic_payment",
  amount: '500',
  id: payment_gateway ,
  default: 'true'
%}
```
{% endcode %}

Instead of "test", use something private to you, so malicious users don't discover it and cause confusion by making test payments.  But this example will keep using "test".\
\
4\) Now in Siteglide create a second payment gateway, and mark as enabled and test mode true. You can use the same test keys as your main payment gateway. This needs to be done after step 3 or Siteglide won't know which gateway to use.\
\
5\) Finally, visiting the page with \`?test=2\` where 2 is the payment gateway ID of your test gateway, will load the page and form in test mode.\
\
A variation of this technique is possible using a copy of the page rather than URL query parameters.\
\
\

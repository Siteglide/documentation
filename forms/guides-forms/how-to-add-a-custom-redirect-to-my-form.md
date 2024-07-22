# 📋 Steps to Programmatically  Redirecting after a Form Submission

On Forms you can set the default redirect in the Form Builder view in Siteglide.

However, if you wish to make this redirect dynamic, you can instead include a hidden field on the Form and set the redirect value there.

## Step 1) Add an s\_redirect input field to the form

```html
<input 
  id="s_redirect" 
  value="/home" 
  type="hidden"
/>
```

This example will redirect the user to `/home` no matter what the redirect says in Siteglide Admin. You can alter this value with JavaScript should you wish to have a dynamic redirect.

## Step 2) Add JavaScript Logic to Adjust the value of the field based on some event

{% tabs %}
{% tab title="Liquid" %}
```liquid
<select id="choose_office" required>
    <option value="1">Office 1</option>
    <option value="2">Office 2</option>
</select>
<input 
  id="s_redirect" 
  value="/home" 
  type="hidden"
/>
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const select = document.querySelector('#choose_office');
const redirect = document.querySelector('#s_redirect');
select.addEventListener('change', function(e) {
  const t = e.currentTarget;
  const v = t.value;
  if(v === '1') {
     redirect.value = '/confirm-office-1';
  } else if(v === '2') {
     redirect.value = '/confirm-office-2';
  }
});
```
{% endtab %}
{% endtabs %}

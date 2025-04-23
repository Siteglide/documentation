# Forms Above the Fold

Adding a Siteglide form in a Page shouldn't have a significant impact on speed in most cases. \
\
However, if your homepage includes the reasonably common design of including a form in the hero section, and this form contains an hcaptcha widget to reduce spam, it could affect your First Contentful Paint (FCP) score. This is because bots are now getting so sophisticated, that the captcha widget includes a large download. You want to be loading this after the FCP, but it's tricky if the form is above the fold as the browser will wait for it.\
\
A common design pattern to get around this is to use a short, static form in the top of the homepage to hook the user in and then redirect a user to a longer form. To make this easier to use, the main form should autofill any information they've already entered.\
\
1\) Create your main form on a contact or newsletter page, - and on the homepage itself use an HTML form with a single email field and an action parameter which leads to the contact page. This form does not need spam protection, since it's not yet submitting information to the server, meaning it's a lot faster to load.

```
<form method="get" action="/newsletter">
  <input name="email" type="email">
  <input type="submit" value="Sign Up">
</form>
```

Style and add labels as needed.\
\
2\) Optional- advanced step requiring Siteglide-CLI. If you're confident you're not going to include any Siteglide forms on this page now, you can disable Siteglide JS for the page, which will make it even faster. If you have other forms in the footer or lower in the page, skip this step, as they require the JS.\
\
In the top of the page in CLI, add the use\_siteglide\_js setting and set to false.

```
---
use_siteglide_js: false
layout: templates/1
metadata: 
---
```

The existing yml settings should not be changed, the above is an example only.

3\) Add your main form to the \`/newsletter\` page. When the user submits the homepage form, it will navigate them to:\
\
\`/newsletter?email=\<users\_email>\`\
\
4\) In the form layout, set the \`value=""\` HTML attribute on the s\_email field to the value submitted in the form. This will save the user entering the data twice.

```
<input name="s_email" value="{{context.params.email}}">
```

# Image Transformations Reference

## Generating a single link to a single version of an image: `img_url`

This tag can be used as a direct replacement\* for the `| asset_url` filter, which is used to transform a relative path to an image into an absolute link to a cached asset. \*Only for images. PDFs, stylesheets, scripts, videos and other non-image assets should continue to use `| asset_url` .

Using this on its own is probably quick and convenient in some cases, but in many cases you can probably get better results out of the browser by wrapping several of these links to the same image in an [`img` include tag's Liquid layout](image-transformations-reference.md#providing-the-browser-with-multiple-versions-of-an-image-using-a-liquid-layout-img) to provide the browser with multiple versions of the image and giving it hints on which to use in each situation.&#x20;

In these examples, let's assume that we have an images folder in File Manager and we uploaded a single high-quality file called `high-quality-image.jpg`&#x20;

Basic example:

```liquid
{% include 'img_url', path: 'images/high-quality-image.jpg' %}
```

Example using all available parameters:

```liquid
{% include 'img_url', path: 'images/high-quality-image.jpg', options: 'format=auto,width=300,height:400,fit:crop' %}
```

Parameters explained:&#x20;

<details>

<summary>path - required - String</summary>

The path to your image. This should be a relative path to your image in File Manager, relative to the assets folder (File Manager's root). It should include the original file extension e.g. .jpg\
\
It should not start with:\
\- A leading forward slash `/`\
\- `/assets`\
\- `marketplace_builder`

If you have a path to an image in a Liquid variable, for example if using data from a WebApp, you can set the value of path directly to this variable without using quotes.\
\
This is the same format as you may have been familiar using before an `| asset_url` Liquid filter.&#x20;

</details>

<details>

<summary>options - optional - String (comma-separated key-value pairs with <code>=</code> signs)</summary>

These refer directly to Cloudflare's [Image Transformation options](https://developers.cloudflare.com/images/transform-images/transform-via-url/#options) and they will appear in the final URL generated in the tag. As Cloudflare add more parameters in future, you can safely use them here. \
\
For each option you want to include, assign each value to its key using an `=` sign. Separate each option with a comma.&#x20;

To save time, you can choose to leave options blank, see basic example. Our default options will then be passed: \`

```liquid
format=auto,width=auto
```

To help Cloudflare make `auto` as smart as possible at predicting what size the image should be, we automatically add meta-tags to Siteglide Head Scripts which use the new feature of browser hints- at time of writing this is only supported on Chromium based browsers.&#x20;

</details>

## Providing the browser with multiple versions of an image using a Liquid layout: `img`&#x20;

This feature allows you to use layouts which contain best-practice HTML like \`srcset\` and then re-use them throughout your site. We have created some default layouts which cover a few common types of image, but feel free to make copies of these in order to edit them for your specific site.&#x20;

Basic example:

```
{% include 'img', path: 'images/high-quality-image.jpg' %}
```

Example using all available parameters:&#x20;

```
{% include 'img', path: 'images/high-quality-image.jpg', attributes: 'loading="lazy" data-custom-value="custom"', classes: 'custom-css-class custom-css-class-2', layout: 'default/base', any_custom_liquid_variable: 'custom_value'  %}
```

Note `options` is _not_ listed as a parameter here. This is because, inside a layout, multiple `img_url` tags are expected, each with _different_ Cloudflare options. You can however use custom Liquid parameters to pass into your own layouts data which might determine which options might be used.&#x20;

Parameters explained:

<details>

<summary>path - required - String</summary>

(This is the same type of parameter as is used in the `img_url` include tag. In most cases the `img` include tag will directly pass this value to all of the `img_url` tags inside its layout.)\
\
The path to your image. This should be a relative path to your image in File Manager, relative to the assets folder (File Manager's root). It should include the original file extension e.g. .jpg\
\
It should not start with:\
\- A leading forward slash `/`\
\- `/assets`\
\- `marketplace_builder`

If you have a path to an image in a Liquid variable, for example if using data from a WebApp, you can set the value of path directly to this variable without using quotes.\
\
This is the same format as you may have been familiar using before an `| asset_url` Liquid filter.&#x20;

</details>

<details>

<summary>attributes - optional - String</summary>

Default: `` 'loading="lazy"` ``\
\
This allows you to pass in any HTML attributes into the layout. Most layouts will use an `<img>` HTML tag and will output these attributes into that tag, but check the layout file itself.

For images above the fold, it is recommended (though not essential) that `loading="lazy"` is not set on an img tag. You can set the `attributes` parameter to an empty String `''` if you think the image is likely to appear above the fold.\
\
This allows you to add in features like [https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img#fetchpriority](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img#fetchpriority) which can be added as attributes to the img tag.\
\
It also allows you to add important accessibility features like the `alt`  or `title`  attributes.

</details>

<details>

<summary>classes - optional - String</summary>

Default: `''` (empty)

&#x20;This allows you to pass in any CSS classes into the layout, to be inserted into the main element's class attribute.  Most layouts will use an `<img>` HTML tag and will output these classes into that tag, but check the layout file itself to confirm.

</details>

<details>

<summary>Custom Liquid Parameters</summary>

As with any Liquid include tag, you can explicitly pass in any custom parameters you like, with some rare exceptions. You might find this especially helpful here, to pass in image-specific information when it is known e.g. width and height - but only where the layout itself is expecting these variables.

Some of our default layouts are set up to expect a custom Liquid parameter of `width`, but have defaults in case this is not passed. This has not been made an official parameter in order to make the layouts themselves as flexible as possible, however some user-interfaces in future may treat it as such for convenience.

</details>

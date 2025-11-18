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

<summary>options - optional - String (comma-separated key-value pairs with `=` signs)</summary>

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

```liquid
{% include 'img', path: 'images/high-quality-image.jpg' %}
```

Example using all available parameters:&#x20;

```liquid
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

<summary>layout - optional but recommended - String</summary>

Leaving this blank will output a basic HTML `img` tag with a single `src`  image - which will be given the default Cloudinary transforms from `img_url`.\
\
You can set this to any layout you create , or use one of our default layouts documented below.

You can reference a layout by its path relative to (but not including) the `layouts/img` folder.

</details>

<details>

<summary>Custom Liquid Parameters</summary>

As with any Liquid include tag, you can explicitly pass in any custom parameters you like, with some rare exceptions. You might find this especially helpful here, to pass in image-specific information when it is known e.g. width and height - but only where the layout itself is expecting these variables.

Some of our default layouts are set up to expect a custom Liquid parameter of `width`, but have defaults in case this is not passed. This has not been made an official parameter in order to make the layouts themselves as flexible as possible, however some user-interfaces in future may treat it as such for convenience.

</details>

### Custom Layouts

Layouts should include best practice HTML and almost always&#x20;

```liquid
{% include 'img_url' %}
```

&#x20;tags to provide different alternative versions of the same image within that HTML.

Layouts should be a single Liquid file, with a name of your choice, inside the in the `marketplace_builder/views/partials/layouts/img/` folder.

### Out of the box - Default Layouts

The default layouts have been built with inspiration from this page from Cloudflare: [https://developers.cloudflare.com/images/transform-images/make-responsive-images/](https://developers.cloudflare.com/images/transform-images/make-responsive-images/). For those new to the `srcset` and `image-set` options in HTML and CSS respectively, it's only possible for the browser to choose which responsive image to use based on a single criteria- either whole screen width or the pixel density (dppx) of the screen. Depending on the size of image, different layouts will get better results (and you are of course encouraged to improve on what is provided here).&#x20;

#### default/lg

`lg` stands for large. This layout is designed with images in mind which are intended to be full-screen-width on any device - think hero images (unless they are background images).&#x20;

The `srcset` will pass multiple sizes of the image to the browser and the browser will pick the best one depending on the width of the entire screen.\
\
Recommended use:

```liquid
{% include 'img', path: 'images/high-quality-image.jpg', layout: 'default/lg' %}
```

#### default/base

Intended for medium size images where the HTML `img`  element will have a set maximum width, default `640` px. The point of the max width really is where you don't actually want a full-screen-width image on desktop, though it might be on smaller screens. If you do want a full-width image, the `default/lg` option will be more appropriate.

The `srcset` will pass multiple sizes of the image to the browser and the browser will pick the best one depending on the width of the entire screen, with the caveat that it will not pick one wider than the max-width set.

Recommended use (note the custom parameter expects an integer for the max-width, and the parameter is named just `width`):

```liquid
{% include 'img', width: 800, path: 'images/high-quality-image.jpg', layout: 'default/lg' %}
```

#### default/sm

`sm` stands for small.&#x20;

Intended for small images and thumbnails where there is a lot of room to shrink the image and seriously boost page speed, but at the same time you want to preserve quality on high-definition e.g. 2dppx displays.

The different versions passed to the browser depend on the screen's pixel per inch property, rather than on the width of the entire screen. This is because the image is likely to be a lot smaller than the screen width, so basing the size on the screen width will most likely be wasteful, whereas without taking into account the screen's definition there is a risk of blurry thumbnails that are not providing enough real pixels to fill out the space on the page.&#x20;

Recommended use (note the custom parameter expects an integer for the width, though if you accidentally provide a String, it will attempt to convert it):

```liquid
{% include 'img', width: 40, path: 'images/high-quality-image.jpg', layout: 'default/lg' %}
```

#### default/sm\_bg

This layout is a little different as it does not include an HTML `img` tag, rather a `div` tag with a background image in the style attribute.

It is not as sophisticated as some of the other examples and may not suit all background images because at the present time of writing, `image-set` only supports choosing a version based on the screen definition, not based on the entire screen width, see: [https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set](https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set). Nevertheless, we wanted to provide an example for this common use case. You may wish to adapt this based on the kind of background images your site uses.&#x20;

Like `default/sm` this layout expects a width custom parameter and optimises based on dots per pixel (ddpx) of the screen:

```liquid
{% include 'img', attributes: '', width: 1000, path: 'images/high-quality-image.jpg', layout: 'default/lg' %}
```

If you just want a full-screen background image, it is probably easier to directly use `img_url` for example:

```liquid
<div style="background-image: url('{% include 'img_url', path: 'images/high-quality-image.jpg', options: 'fit=cover,width=auto' %}')
background-repeat: no-repeat; background-size: cover; background-position: center center;">
</div>
```

The `width=auto`  should optimise well to the screen width on browsers which support browser hints, at the time of writing Chromium browsers.

---
description: >-
  In this guide, we'll add an image to file manager and add it to a page with
  some automatic optimisation for image size and format.
---

# Getting Started with Image Transformations - Full Width "Hero" Images Guide

## TLDR Summary

For a full-width or near full-width "hero" image, we recommend an include `img` tag with a `default/lg` layout:

```
{% include 'img', path: this.image, layout: 'default/lg' %}
```

Other guides will show other kinds of images and more optimal ways to output them.

## Steps

1. Upload an Image

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

In this example we'll add `meercats.jpg` inside the images folder.

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

And it appears in the list like so:

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

The file is large: 3.68mb at 5184px x 3456px. So it will look great but is in need of some re-sizing for almost any use-case. The jpg file type is very common, but it's not the most efficient way to store an image for the web nowadays- usually webp and other next-gen formats can store the same image in a smaller number of megabytes - and are still baseline supported on all major browsers.

However, we don't want to do any manual re-sizing and converting, we can just use this single image and optimise it on the front-end.&#x20;

2. Create (or Edit) a Page

For this example, we'll create a page using Siteglide Studio, but you can create a standard page if you prefer or use an existing page. You can skip this step 2 if you already know how to set up a page.\
Firstly we'll check in Site Settings's Modules Tab that the Studio Module is already downloaded.

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Next, we'll go to CMS/Studio Themes and create a Theme from the Photography Theme in marketplace. (If you already have a Theme please skip).

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Now we can go to CMS/Pages and create a new page with our new Studio Theme:

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

After saving, you'll be sent to the Studio tab.

3. Adding a hero image

We'll add an existing hero section to our Studio page, which uses a large background image:

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Let's use our large example image:

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

At the time of writing, if I view the page, and inspect the image on the page, the image is still being downloaded full size, even though this is unnecessary. (In future, we will update Studio Themes to use optimised images out of the box. So you may find this is not the case when following these instructions in future)

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

4. Modify the Hero Section Code to use an optimised version of the image for the background.

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Switch to code view to modify the code directly.

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

#### What is the situation before we make any changes?

The code currently uses the `| asset_url` filter to convert a relative link to the image from the section fields to an absolute link to the full size image on the CDN.&#x20;

The code:

```liquid
<section class="relative bg-white">
  <div class="relative mx-auto flex w-full h-auto md:h-[890px]">
    <div class="hidden md:block bg-white w-2/12 h-full"></div>
    <div class="py-4 md:py-0 w-full h-auto max-h-48 sm:max-h-80 md:w-10/12 md:max-h-none md:h-full relative border-l-2 border-black">
      <img src="{{ this.image | asset_url }}" alt="{{ this.image_alt }}" class="object-cover object-center w-full h-full">
    </div>
  </div>
</section>
```

The value of `this.image` is the relative path to our image: `images/meercats.jpg`&#x20;

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

After the filter is applied, the result in the HTML code in the browser is an absolute URL to the original version of the file on the CDN:

```html
<img src="https://files.uk-siteglide.com/instances/36/assets/images/meercats.jpg?updated=1756294663" alt="Hero Image" class="object-cover object-center w-full h-full">
```

The exact URL will depend on your site.

#### Let's change this to get a different version of the image automatically depending on the size of the screen:

Replace:&#x20;

`<img src="{{ this.image | asset_url }}" alt="{{ this.image_alt }}" class="object-cover object-center w-full h-full">`

&#x20;with:

```
{% include 'img', path: this.image, layout: 'default/lg' %}
```

This will now change the final rendered HTML to the following:

```html
<img loading="lazy" class="" width="100%" src="https://files.uk-siteglide.com/cdn-cgi/image/format=auto/instances/36/assets/images/meercats.jpg?updated=1756294663" srcset="
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=320/instances/36/assets/images/meercats.jpg?updated=1756294663   320w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=640/instances/36/assets/images/meercats.jpg?updated=1756294663   640w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=960/instances/36/assets/images/meercats.jpg?updated=1756294663   960w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=1280/instances/36/assets/images/meercats.jpg?updated=1756294663 1280w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=2560/instances/36/assets/images/meercats.jpg?updated=1756294663 2560w
  ">
```

5. The Result

With one line of Liquid code, we now give the browser multiple possible links to the image. Each link is similar, but the URL contains different "options". The browser is able to decide which version of the image it should use, according to the width of the screen. On my desktop monitor which has a 2560 x 1080 resolution, the image downloaded is actually the maximum allowed by the HTML: 2560 x 1706.

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Furthermore, the format is automatically converted to webp. The result of both those changes is that the 3.68mb file we uploaded to file manager only required 853kb to load.&#x20;

After a version of an image has been requested once, Cloudflare will cache this image version, meaning future identical requests will be faster and the transformation won't need to be calculated again.

What about mobile? Simulating an iPhone 12 Pro in Chrome, the image is loaded at a smaller size and with a different format (the original format - at some sizes, old formats may still beat modern formats and Cloudflare works this out for you).&#x20;

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Now it's only 264kb!

6. Adding some options.&#x20;

Since we replaced custom HTML with a default `img` layout in the example above, we should feed in a few extra parameters so we can re-add classes and image alt text.

```
{% capture attributes %}alt="{{this.image_alt}}"{% endcapture %} 
{% include 'img', path: this.image, layout: 'default/lg', attributes: attributes, classes: 'object-cover object-center w-full h-full' %}
```

Now our HTML is closer to what we had originally, maintaining accessibility and styling:

```
<img alt="Hero Image" class="object-cover object-center w-full h-full" width="100%" src="https://files.uk-siteglide.com/cdn-cgi/image/format=auto/instances/36/assets/images/meercats.jpg?updated=1756294663" srcset="
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=320/instances/36/assets/images/meercats.jpg?updated=1756294663   320w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=640/instances/36/assets/images/meercats.jpg?updated=1756294663   640w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=960/instances/36/assets/images/meercats.jpg?updated=1756294663   960w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=1280/instances/36/assets/images/meercats.jpg?updated=1756294663 1280w,
    https://files.uk-siteglide.com/cdn-cgi/image/format=auto,width=2560/instances/36/assets/images/meercats.jpg?updated=1756294663 2560w
  ">
```

## Next

Wondering how to adapt this for thumbnails? keep reading:&#x20;

{% content-ref url="../optimising-images-natively-with-cloudflare/optimising-thumbnails-and-medium-sized-images-guide.md" %}
[optimising-thumbnails-and-medium-sized-images-guide.md](../optimising-images-natively-with-cloudflare/optimising-thumbnails-and-medium-sized-images-guide.md)
{% endcontent-ref %}

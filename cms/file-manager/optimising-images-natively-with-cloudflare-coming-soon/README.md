---
description: >-
  How to optimise your images the easy way. Continue to host only a single copy
  of each of your high-quality images on File Manager and have the optimisation
  on the page taken care of with minimal code.
---

# Optimising Images Natively with Cloudflare

## Prerequisites

You can use any of the code described within this document even if you don't meet the pre-requisites. In this case, we will fall-back to a supported alternative, and your image should still display, though un-optimised. This can be useful if you intend to set up image optimisation before copying your site to a new stack.

* You need to have a website on one of our new Oracle and Cloudflare-powered Production stacks before you can take full advantage of this feature. At the time of writing, this option is only available on servers based in London. Please let us know if you'd like access to Oregon or Sydney sooner and we'll be sure to keep you updated.
* Currently this method of image optimisation will only support images stored in Siteglide's file manager. If an absolute path to an image is passed to a tag, we will fall back to returning the URL un-optimised.

## About&#x20;

While many of your clients' devices are getting faster year-on-year, optimising images is still a good way to improve everyone's experience of a website. It not only significantly boosts mobile page speed and associated SEO, but even saves your visitors money on their mobile phone data usage. There are many options for achieving this, but many of them are time-consuming, especially if they involve manually resizing and maintaining multiple versions of each of your images.

The best solutions will allow you to:

* Upload one single version of each image to File Manager and
  * Automatically resize it on the fly when the browser needs it
  * Automatically change its format to next-generation image formats to reduce the size while maintaining the size and quality.
  * Cache any transformations made, so that the next time the image is delivered, it will be as fast as if no transformation had been necessary.
* Conveniently re-use best-practice HTML code for letting the browser know which version on an image to load

### Differences between Cloudflare Image Optimisation and Cloudinary

We have in the past documented how to achieve image optimisation using a 3rd party service like Cloudinary, allowing you to upload which is still a great option which achieves to goal of allowing you to upload one version of an image and transform it on the fly.&#x20;

The advantages of our new Cloudflare offering are:

* Cost / Convenience - since this is built into our Oracle / Cloudflare stacks, there is no need to create a 3rd party account or pay for usage upgrades regarding this.&#x20;
* We have built Liquid tags to allow for best-practice HTML to be inserted as seamlessly as possible into your pages, with sensible defaults which can be overridden easily with well-documented Cloudflare transformations. This means you can optimise images as easily as you once added `| asset_url`&#x20;

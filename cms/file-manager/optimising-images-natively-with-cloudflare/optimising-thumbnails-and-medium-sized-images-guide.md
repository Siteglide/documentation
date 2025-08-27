# Optimising thumbnails and medium-sized images - Guide

## TLDR - Summary

### Thumbnails

For thumbnails, we recommend the following Liquid:

<pre class="language-liquid"><code class="lang-liquid"><strong>{% include 'img', path: this.image, layout: 'default/sm', width: 40 %}
</strong></code></pre>

You can set the width to the size you want the thumbnails to be displayed. The browser will download an image of this size, unless the user has a high resolution screen, in which case it will download a larger version of the image to keep the quality high.

### Medium-Sized Images

For images which are displayed larger than thumbnails and may be full-width on mobile, but may be displayed smaller than full-width on desktop, we recommend our `default/base` layout:

```liquid
{% include 'img', path: this.image, layout: 'default/base', width: 600 %}
```

The browser will load a version of the image responsively, but it will never load one wider than the max-width you provide.&#x20;


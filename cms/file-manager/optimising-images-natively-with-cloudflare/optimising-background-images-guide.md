# Optimising Background Images - Guide

## TLDR Summary

### Thumbnail and Medium-Sized Background Images

Note the width here is the size of the image that will be requested for 1dppx screens.

```liquid
{% include 'img', width: 1000, path: 'images/high-quality-image.jpg', layout: 'default/sm_bg' %}
```

### Full-width Background images

CSS `image-set` does not currently support responsive images by screen width, so we don't currently have a layout for this scenario. It is probably easier to link to a single Cloudflare version of the image source, with automatic optimisation. You can then add any HTML you want:

```liquid
<div style="background-image: url('{% include 'img_url', path: 'images/high-quality-image.jpg', options: 'fit=cover,width=auto' %}')
background-repeat: no-repeat; background-size: cover; background-position: center center;">
</div>
```

See the reference for more information about including links to versions of the image directly:

{% content-ref url="image-transformations-reference.md" %}
[image-transformations-reference.md](image-transformations-reference.md)
{% endcontent-ref %}

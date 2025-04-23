---
description: Tips for speeding up pages which include a video from YouTube or Vimeo.
---

# Video Embeds

HTML5 can play videos, but performance can be improved by using a service like YouTube or Vimeo to embed the video, buffering and streaming parts of the video at a time. They also come with lots of useful player features. \
\
However, what you don't want is loading the video player to slow down the initial rendering of your page, especially when it slows key metrics like FCP (First Contentful Paint).

Using these 3rd party packages can help using "progressive enhancement" to load the player in the background, but display a fallback solution straight up so that FCP is much faster:\
\
\- [https://github.com/paulirish/lite-youtube-embed](https://github.com/paulirish/lite-youtube-embed)\
\- [https://github.com/luwes/lite-vimeo-embed](https://github.com/luwes/lite-vimeo-embed)

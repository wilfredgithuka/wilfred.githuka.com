---
title: Photoswipe Gallery Sample
subtitle: Making a Gallery
date: 2017-03-20
tags: ["example", "photoswipe"]
draft: true
---

Beautiful Hugo adds a few custom shortcodes created by [Li-Wen Yip](https://www.liwen.id.au/heg/) and [Gert-Jan van den Berg](https://github.com/GjjvdBurg/HugoPhotoSwipe) for making galleries with [PhotoSwipe](http://photoswipe.com) . 

{{< gallery caption-effect="fade" >}}
  {{< figure thumb="-thumb" link="/img/gallery/image1.jpg" >}}
  {{< figure thumb="-thumb" link="/img/gallery/image2.jpg" caption="Sphere" >}}
  {{< figure thumb="-thumb" link="/img/gallery/image3.jpg" caption="Triangle" alt="This is a long comment about a triangle" >}}
{{< /gallery >}}

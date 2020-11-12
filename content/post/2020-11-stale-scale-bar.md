---
title: "Creating vintage, stale scale bar"
subtitle: "A small follow-up of the stale map"
description: "A small follow-up of the stale map"
date: 2020-11-11
draft: false
categories: ["Jot"]
tags:
  - ArcGIS Pro
  - Cartography
image: "../post/2020-11-stale-map-follow-up/scale-bar.jpg"
---

A small follow-up on the old stale map, with a new scale bar

<!--more-->

---

[John Nelson](https://www.esri.com/arcgis-blog/author/j_nelson/) published two new video tutorials on creating hand-drawn vintage scale bars. I find this is the right time to revise my previous stale map - the scale bar looks too perfect and inorganic.

{{<youtube eJPHQCGjvuQ >}}

<br>

{{<youtube eTQTvP7QqfA >}}

I then followed the guides and replicated the same scale bar style in my original stale map project. At least it doesn't look bad. The red fill colours may need some further refinements - the fill looks a bit too perfect for me. I sort of want the fill to be "scrapped off" a bit with only the colour of the paper left behind.

{{< figure src="/post/2020-11-stale-map-follow-up/scale-bar.jpg" height="50%" width="50%" >}}


What I learnt is about the advanced formatting options in Pro. Specifically, _Pro treats words as polygon objects_. I never knew about this before and have no idea how to add filter (sort of like transforming a rasterised object in Photoshop) to words.

Besides, I finally get the basis of making the lines less artificial and more hand-drawn. I would summarise the points as:

1. Add a random wave filter, adjust period of amplitude
2. Change the opacity of the line
3. Duplicate the line
4. Change the duplicated line to "dotted" line. This simulates how the ink "stops" in part of the line
5. Readjust opacity, period and amplitude of the random wave

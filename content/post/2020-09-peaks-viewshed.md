---
title: "Viewshed From Peaks"
summary: "Quick round up of an interactive web map project"
date: 2020-09-13T19:47:11+08:00
subtitle: "Interactive web application"
description: ""
draft: false
categories: ["Behind the Scene"]
tags:
  - ArcGIS API
  - Javascript
  - Web Map
image: "2020-09-peaks-viewshed/HKPeaks_Overview.png"
---

I made an interactive web map a few months before as a little project to practise some Javascript and web mapping skills.

{{% button href="https://khwong12.github.io/HK_Peaks/" icon="fas fa-map" %}}**Play the Interactive Map**{{% /button %}}

The project was originally a random thought when I was on a hike to Lion Rock on June.

Most of the tasks I've been doing are data analysis and some static data visualisations. Even for interactive web maps, I have only used the web apps already provided in ArcGIS Online. They are some ready-to-go applications - once you pushed the spatial data to the online cloud, you just need to add the data to the application template. I would say those applications serve 90% of the common tasks.

Still, I would like to try making a custom web map with javascript. Thus I made this web map.

The base of the code is from the code sample of computing viewshed available on ESRI's website. The base of the web map is also of course comes from the code sample. I spent most of the time reading and trying to understand how those *listener* functions are doing. Those `view.on()` and `view.goTo()` functions takes me a while to understand what they are doing.

Still need more time to consolidate my concepts on the async properties related to client-side mapping.

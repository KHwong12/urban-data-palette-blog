---
title: "Tools for Generating Public Transport Isochrone Maps"
subtitle: "On the journey of finding public transport data routing services for Hong Kong"
description: ""
date: 2020-12-10
draft: false
categories: ["Jot", "Usage Report"]
tags:
  - Isochrone Map
  - Routing
  - Accessibility
  - Public Transport
image: "2020-12-public-transit-isochrone/traveltime-test.png"
---

A few notes on finding tools to create isochrone map with public transit travel time

<!--more-->
---

I have a new project which needs to generate some [isochrone maps](https://wiki.openstreetmap.org/wiki/Isochrone). To be honest, isochrone maps sounds like a jargon for me - I find the term **Travel Time Map** more explicit and easy to understand. Originally, I call this type of map "Service Area map" since I usually make these maps in ArcMap/ArcGIS Pro with the network analyst extension. And that's [how ESRI calls this type of map](https://desktop.arcgis.com/en/arcmap/latest/extensions/network-analyst/service-area.htm).

![](https://pro.arcgis.com/en/pro-app/help/analysis/networks/GUID-569B9331-C31B-4FA9-835C-EA9D39EB08D0-web.png)
from https://pro.arcgis.com/en/pro-app/help/analysis/networks/service-area-analysis-layer.htm

## Isochrone with Accurate public transit data

The task, of course, is not that simple. My task is to create isochrone maps with the following requirements:

1. The travel time is counted using **public transit**, not private cars/trucks/walking
2. The focus area is in Hong Kong
3. GUI Available (if possible)

In case you don't know, 90% of the journeys in Hong Kong are made using public transit. Public transit in Hong Kong is so convenient and well-maintained that even commuters with driving licenses would still prefer taking MTR. This is always a model for foreign cities aiming to reduce private car usage and promoting green public transport.

But this implies isochrone for cars are not useful when conducting accessibility assessments in Hong Kong - after all, who would take cars? Public transit and walking are the main mode of commuting. This means I have to search for accurate datasets of public transport in Hong Kong to generate those accessible area maps.

I believe Google Maps has the most comprehensive public transport database for routing analysis and commuting data collection in the context of Hong Kong - even more comprehensive than the one owned by the Governmental Departments. However, [Google Map Services API does not provide isochrone generations](https://developers.google.com/maps/documentation/javascript/directions). Google Map API are powerful in terms of geocoding and routing. What a pity that isochrone feature is not available.

I also searched for non-GUI tools like [Valhalla](https://valhalla.readthedocs.io/en/latest/api/isochrone/api-reference/). It could act as a backend for generating these isochrone maps. Still, I do not have much knowledge of C++ and I believe it's not a good idea to trying understand the code of this project. I am more capable of twerking a few JavaScript snippets, not a huge C++ project.

## The attempts

Therefore, I switched back to finding some GUI tools to generate isochrones. This article summarises the tools I have searched for and records my findings.

| Tool/Site | Public transport data available | Global Coverage? (Hong Kong data available) | GUI Available |
| ----------- | ----------- | ----------- | ----------- |
| Open route Services | no | yes | yes |
| Mapnificent | yes | no | yes |
| Traveltime  | yes | no | yes |
| Mapzen | no | yes | yes |
| Mapbox | no | yes | no |



### Attempt 1: Open route Services

https://maps.openrouteservice.org/

When you see some geo-related applications with a word "open", you know it is related to OpenStreetMap. It is unsurprising to see how this service works:

> Openrouteservice is being developed and provided by Heidelberg Institute for Geoinformation Technology (HeiGIT) and offers Routing services by using user-generated, collaboratively collected free geographic data from OpenStreetMap. Please donate your geographic data to openstreetmap.org!

Yet, they only have the following travel options available: car, trucks, bicycle, walking and wheelchair(!). It is already astonishing to provide walking isochrone for a completely free service. However, this is not enough for my task.

Conclusion: **Not Useful**

### Attempt 2: Mapnificent

![](/post/2020-12-public-transit-isochrone/mapnificent-usecase.png)

https://www.mapnificent.net/

Public transit data available! They have already stressed this in the catchphrase.

> Shows you areas you can reach with public transport in a given time.

However, no data available in Hong Kong.

Conclusion: **Not Useful**

### Attempt 3: Traveltime

![](/post/2020-12-public-transit-isochrone/traveltime-usecase.png)

https://app.traveltime.com/

They have public transport option available. There's even an option called *"Driving and Train"*, which may be a common commute option for English citizens.

In addition, I love the UI of this tool. Their colour choice for the buttons and basemap looks pleasant to me. I find colours near navy blue comfortable and "warm".

But the service is limited to Europe.

Conclusion: **Not Useful**

### Attempt 4: Mapzen

![](/post/2020-12-public-transit-isochrone/mapzen-usecase.png)

https://www.mapzen.com/products/mobility/isochrone/

This web map looks great for me. Without doubt it uses **Valhalla** for the backend of the routing services. You are free to click on any point around the globe and check the isochrone of driving, walking and cycling.

However, no public transit data available. And the cut-off travel time seems to be fixed on 15, 30, 45 and 60 mins.

Conclusion: **Not Useful**

### Attempt 5: Mapbox

https://docs.mapbox.com/api/navigation/#isochrone

I love Mapbox in terms of their cartography products. And it's great that they also provide isochrone mapping services. They even have a [demo](https://docs.mapbox.com/playground/isochrone/) for it.

However, only walking, driving and cycling options are available. Not useful when I want to deal with public transit.

Conclusion: **Not Useful**

---

## Results

I believe there are no GUI tools suit my need. I dare.

---

## My planning attempts

But I still have to work on the project. Following are some tools I found yet haven't tried. I will update my usage report when I decided to try them.

### Third-party Google Map Isochrone generation JavaScript

![Eiffel Tower isochrone](https://www.dugwood.com/isochrone-screenshot.png?1520424890)

https://github.com/dugwood/isochrone-isodistance-with-google-maps

It is not a truly isochrone. Isochrone mapping is not supported by Google Map, regardless of being end users or map developers. The polygons are just computed using the distance-matrix approach to generate vertex of the travel-time polygon, with some smoothing algorithm applied.

**Pros**
- Google map API services is used compute public transit travel time

**Cons**
- Time needed to write and debug the codes
- Not sure if the script fits with the latest version of the Google Map API

### GTFS Data with R

https://xang1234.github.io/isochrone/

---
title: "Street Suffixes in Hong Kong"
subtitle: "Visualising and analysing the distribution of street names"
description: ""
date: 2020-05-29
draft: false
categories: ["Map Essay"]
tags:
  - Cartography
  - Data Visualisation
  - Urban Studies
  - Hong Kong
image: "2020-05-street-suffix/CoreUrban_CHIENG.png"
---

How do you like the street naming? On maps.
<!--more-->

<!-- ![CoreUrban_CHIENG](/post/2020-05-street-suffix/CoreUrban_CHIENG.png) -->

## TL;DR

I made an [interactive web application](https://foa-hku.maps.arcgis.com/apps/Compare/index.html?appid=aa9509f071e943edaa926f2159568ea0) and some print maps colouring the Chinese and English suffix of the roads in Hong Kong. I also did some basic analysis.

---

## How are the roads named?

Have you ever noticed the name of the streets you walk by every day? Specifically, what is the **end word** of the street name?

**Street suffixes** are the end words used to describe the characteristics of the street. In Hong Kong, once a new street is officially named, the Lands Department will gazette a series of governmental notices to declare the street name and the exact location and alignments of that street like [this one](https://www.gld.gov.hk/egazette/pdf/20202421/egn202024212656.pdf). The newest Notices and Plans for Street Naming is available in the [Lands Department webpage](https://www.landsd.gov.hk/mapping/en/street_name/str.htm).

Still, there are no laws for the government to follow how the streets should be named. The most relevant legislation related to street names is [CAP132 s.111](https://www.elegislation.gov.hk/hk/cap132!en?xpid=ID_1438402662698_001&INDEX_CS=N):

>(1) Notwithstanding section 111B, the Authority, by declaration in the Gazette, may—
>
>​	(a) assign a name to a street that has not been named; or
>​	(b) change the name of a street that has been named.

Naming new streets are matters mostly related to Lands Department. After a new street is built, Lands Department will circulate the proposed street name to various governmental departments (Post, Home Affairs Department, etc. ) for collecting representations and comments. Once the District Council approves the proposed street name, Lands Department takes the follow-up matters, including gazette and construction of road signs.

<img src="https://i.loli.net/2020/05/29/48EKJNUpyBkLZO3.jpg" alt="st_dhc_2019_017_tc_tcannex_2_page-0002" style="zoom: 33%;" />

Workflow of street naming. from [Annex II of Sha Tin District Council Committees Meetings Discussion Papers](https://www.districtcouncils.gov.hk/st/doc/2016_2019/tc/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_2.pdf) (Only Chinese version is available)

Though there are no laws on street naming, technical memorandums are still available. In 1950s/60s, the Urban Council published several documents about naming rules of streets and the translation between the Chinese and English street suffix. It is still used by Lands Department as a reference for street naming. Still, not many official documents are available about the choice of street suffix. The rules are more de-facto.

---

## How are the street suffixes chosen?

What are the de-facto standards and rules, then? In a District Council meeting about discussing street naming matters, Lands Department provided the following guidelines street suffix types:

> i) Road (道／路) ──區域幹道或市區幹道。
>
> ii) Street (街) ──地區幹道或次要道路，多有樓宇在旁。
>
> iii) Path (徑) ──行人路或小路。
>
> iv) Lane (里) ──通道，或樓宇之間短而狹窄的小路。

*from [Annex III of Sha Tin District Council Committees Meetings Discussion Papers](https://www.districtcouncils.gov.hk/st/doc/2016_2019/en/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_3.pdf) (Only Chinese version is available)*

We could roughly classify the street suffix according to the *hierarchy* of the roads.

"**Highway**" has the highest hierarchy among all carriageways in Hong Kong. Highways are mainly expressways and in the route system.

Roads with the second level of the road hierarchy usually have names ended with "**Road**", "**Avenue**" and "**Drive**". These suffixes are reserved for major thoroughfares. They usually have 2-4 lanes (or more) and serve as the "trunk" and "backbone" roads of the transport system.

What comes next is "**Street**", which are usually residential roads. Sidewalkers are commonly found on the two sides of the roads. "Street" is more common in local residential neighbourhoods. Part of these "Streets" are single lane road and packed with buildings on the two side of the road.

Finally, we have "**Path**" and "**Lane**". These two suffixes mostly refers to local residential pathways, especially **cul-de-sac** with the only exit points towards the major "Road"/"Street" in the district.

These are the most common names you could when you are taking a walk in the city. Besides, there is some standard translation between the Chinese and the English suffix like below. The names follow the common term of 「道路街徑里」, stating the hierarchy of the streets.

- **公路**: Highway
- **道/路**: Road, Drive, Avenue
- **街**: Street
- **徑**: Path
- **里**: Lane

This begs the old-but-gold question of geographers again:

> Where are they, then?

Are they any spatial patterns we could observe about the suffix of the streets?

Transport Department provides a road network open database. After some data cleaning, the dataset includes in total **3,270 roads** in Hong Kong. I then classified the Chinese street suffix into 7 types and English street suffix into 8 as below:

- **Chinese**: 公路、道、路、街、徑、里、其他
- **English**: Highway, Road, Drive, Avenue, Street, Path, Lane, Others

So, what are the spatial patterns of the street suffix? Let's continue...

---

## Maps, Interactive and Print

This is an interactive web map colouring the carriageways in Hong Kong by its Chinese and English street suffix.

{{% button href="https://arcg.is/SviOu" icon="fas fa-map" %}}**Play the Interactive Map**{{% /button %}}

The map on the left-hand side colours the street by their CHINESE street suffix, while the one on the right-hand side is coloured by ENGLISH street suffix. Two maps are synchronised - when you drag on either map, both windows will move/zoom to the same area. You can do some side-by-side comparisons with this application.

When you click on any road, a pop-up will appear on both maps. The pop-up shows both Chinese and English full name of that road. You can interactively click on the roads to check the full name of each road and their respective suffix.

![InteractiveMap](/post/2020-05-street-suffix/InteractiveMap.gif)

If you are not fans of interactive maps, you can check out the static print version of the roads below.

![RoadSuffix_WholeHK_CHI](/post/2020-05-street-suffix/RoadSuffix_WholeHK_CHI.png)

![RoadSuffix_WholeHK_ENG](/post/2020-05-street-suffix/RoadSuffix_WholeHK_ENG.png)



---

## Basic Analysis

The story, of course, would not end by just colouring the streets. What insights do the maps give us? A starting point is always counting the total number of each category.

### How many roads do we have for each CHINESE suffix?

The bar chart below shows the number of each Chinese Street Suffix. Each horizontal bar represents one street suffix type.

Without surprise,「街」 is the most common suffix among all roads, with 1350 thoroughfares falls into this category.「道」and「路」has relatively about the same number. There are 646 roads named 「道」 and 744 roads named 「路」. 110 Streets has the 「徑」 suffix and 216 belongs to「里」.

![Suffix_Chi](/post/2020-05-street-suffix/Suffix_Chi.png)

### How many roads do we have for each ENGLISH suffix?

The bar chart showing the count of each English suffix type is shown below. Same as the one showing the Chinese suffix above, each horizontal bar represent one street suffix type.

Among the roads in Hong Kong, "Road" is the most common suffix. 1363 carriageways have (literally) a "Road" suffix. The second most common suffix is "Street". 1329 thoroughfares has (again, literally) a "Street" suffix. Though drive and avenue are some common suffixes you can find in the urban area, only 34 and 53 thoroughfares are named with "Drive" and "Avenue" respectively.

![Suffix_Eng](/post/2020-05-street-suffix/Suffix_Eng.png)


### What is the relationship between Chinese suffix and English suffix?

The above two are just some starters. Here is the real question when we want to dig deeper:

> What are the differences between Chinese and English Suffix of the Roads?

Here, we classify the streets by both their Chinese and English street suffix. With 7 Chinese and 8 English street suffix groups, we have in total of 56 combinations to identify which group does each street belongs to. In the chart below, each *row* refers to one Chinese suffix category and each *column* refers to one English suffix. Therefore, each *cell* refers to each "Chinese and English suffix combination" of the road. The *colour* of each cell refers to the total number of roads falling into that combination. Darker colour implies a higher number of roads in that category.

Say, the dark purple cell on row 「街」 and column "Street" implies there are 1,327 thoroughfares have a Chinese Suffix of 「街」 **and** English Suffix of "Street". The blueish-green cell on row 「道」 and column "Avenue" means there are 25 thoroughfares with Chinese Suffix of 「道」 and English Suffix of "Avenue".

![Heatmap between Chinese and English suffixes](/post/2020-05-street-suffix/heatmap.png)

Immediately we could draw some interesting insights:

- Majority of the 「公路」 does have an English Suffix of "Highway"; Instead, they are just called "Road"
- Paths with the suffix of "Streets" mostly (as expected) has the Chinese suffix of 「街」
- "Path" is mostly equivalent to 「徑」, while "Lane" has usually the same meaning as 「里」
- "Drive" applies to both higher hierarchy roads of 「道/路」and lower hierarchy roads of 「徑」 at the same time

The fun (and chaotic) part is the difference between 「道」and「路」. These two characters are interchangeable in Chinese word sense. Even 「道路」 exactly means "road" in Chinese! Besides, the government assumes these two words are interchangeable. One direct observation is that 「道」 refers to roads in the urban area of Hong Kong Island and the Kowloon Peninsula. 「路」 refers to roads in New Territories, especially those in New Town. (Check the map again!)

But why the government named those in urban area differently than those in New Territories? That would be another story... probably a research topic for urban historians.

---

## Hiatus

Streets are named by the government and the people. And street names are part of urban history. This somewhat implies the naming system is inevitably chaotic.

Still, when mapping things out, we can try to understand some of the basic patterns inside the chaos. Spatial data and maps are always the tools to help us effectively understand things happening in the cities. It does not need to be policy-related only. Things related to urban are spatial data, and you can always draw it out.

Let the mapping journey continues!

---

## References

The series of Annex about Street Naming, by Lands Department:

- https://www.districtcouncils.gov.hk/st/doc/2016_2019/en/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_1.pdf
- https://www.districtcouncils.gov.hk/st/doc/2016_2019/en/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_2.pdf
- https://www.districtcouncils.gov.hk/st/doc/2016_2019/en/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_3.pdf
- https://www.districtcouncils.gov.hk/st/doc/2016_2019/en/committee_meetings_doc/DHC/15566/st_dhc_2019_017_tc_tcannex_4.pdf

馬冠堯：約定俗成的街道命名做法

- http://www.hkumachsaa.org/622?fbclid=IwAR31GeSLslWVnl9rA74qiXVkyXLbynTNncnfH4AVZQqufvyvUeFhJeAsT_s

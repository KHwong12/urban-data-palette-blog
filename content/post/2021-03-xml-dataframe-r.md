---
title: "Converting nested XML to dataframe in R - a tidyverse approach"
summary: "Transforming XML to tidy data (and csv)"
description: ""
date: "2021-03-04"
draft: false
categories: ["Data manipulation", "R"]
tags:
  - xml
  - R
  - tidyverse
  - data manipulation
image: "2021-03-xml-dataframe-r/xml-to-dataframe.png"
---

## TL;DR

**tidyr** (in tidyverse) provides functions `unnest_wider` and `unnest_longer` to transform XML data into dataframe quickly, using the same ideology of `pivot_wider` and `pivot_longer` in **dplyr**.

---

I rarely deal with XML data. However, sometimes the government discloses open data in XML format only. Currently I need to find data about the restaurant licenses in Hong Kong, and FEHD provides an [open dataset](https://data.gov.hk/en-data/dataset/hk-fehd-fehdlmis-restaurant-licences/resource/05053ecc-623a-415f-b703-5f785edd482c). Unluckily, the dataset is available in XML format only.

The xml data file looks like something below:

![](/post/2021-03-xml-dataframe-r/xml-view.png)
<figcaption>xml of the restaurant license data</figcaption>

The tree strucutre of the XML is in the below form:

- DATA
  - DEPARTMENT
  - GENERATION_DATE
  - LINK
  - TYPE_CODE
  - DIST_CODE
  - INFO_CODE
  - LPS
    - LP
      - TYPE
      - DIST
      - LICNO
      - SS
      - ADR
      - INFO
      - EXPDATE

**DEPARTMENT**, **GENERATION_DATE** and **LINK** are metadata. **TYPE_CODE**, **DIST_CODE** and **INFO_CODE** are data dictionary to store the ID used to encode data. Therefore, only the parts wrapped inside hte **LPS** is the "actual" data I need.

---

## Transform xml to dataframe with R

```r
library(xml2)
library(tidyverse)
```

First thing first, load the packages.

### Transform xml to list

```r
xml_address = "http://www.fehd.gov.hk/english/licensing/license/text/LP_Restaurants_EN.XML"

restaurant_license_xml = as_list(read_xml(xml_address))
```

Here `read_xml` from **xml2** is used to read the xml file. The `as_list` function then turn it into an equivalent R list.

### Expand the data to multiple rows by tags

```r
xml_df = tibble::as_tibble(restaurant_license_xml) %>%
  unnest_longer(DATA)
```

The xml becomes an extremely long list. As the xml is nested into multiple layers, the thing to do is to unnest the first layer. `unnest_longer` is a function in tidyr which unnest a list the split the values of the list to multiple rows (thus *longer*).

**DATA** in the parameter of `unnest_longer` refers to the **DATA** tag on the top layer of the xml. When it is unnested, the structure of the dataframe will return the data inside each tag. In addition, a new column named **DATA_id** is added to indicate which xml tag the data belongs to. Since we are unnesting the first layer, the **DATA_id** column includes these 7 values:

  - DEPARTMENT
  - GENERATION_DATE
  - LINK
  - TYPE_CODE
  - DIST_CODE
  - INFO_CODE
  - LP


![](/post/2021-03-xml-dataframe-r/unnest-longer.png)
<figcaption>Unnest the xml list into longer form</figcaption>

The data of each LP tag is in a list form like this:

```r
list(
  TYPE = list("MR"),
  DIST = list("15"),
  LICNO = list("3715038319"),
  SS = list("Jumbo"),
  ADR = list("JUMBO FLOATING RESTAURANT, ABERDEEN TYPHOON SHELTER, SHUM WAN, WONG CHUK HANG, SOUTHERN, HONG KONG"), 
  INFO = list("#F#G#H"),
  EXPDATE = list("2021-06-30")
)
```

Compare to the xml version of the data:

```xml
<LP>
  <TYPE>MR</TYPE>
  <DIST>15</DIST>
  <LICNO>3715038319</LICNO>
  <SS>Jumbo</SS>
  <ADR>JUMBO FLOATING RESTAURANT, ABERDEEN TYPHOON SHELTER, SHUM WAN, WONG CHUK HANG, SOUTHERN, HONG KONG</ADR>
  <INFO>#F#G#H</INFO>
  <EXPDATE>2021-06-30</EXPDATE>
</LP>
```

The structure of the data is thus the same. Still, it is easier to work with list in R.

### Expand the data to multiple columns by tags

```r
lp_wider = xml_df %>%
  dplyr::filter(DATA_id == "LP") %>%
  unnest_wider(DATA) 
```

First, data not in the **LP** tags are discarded using `dplyr::filter`. Then, I need to expand the attributes of each license into each column (i.e. a column for TYPE, another column for DIST, etc.). Unlike the step above, this time `unnest_wider` is used to "expand" the data in a single column to multiple columns (thus *wider*).

![](/post/2021-03-xml-dataframe-r/unnest-wider.png)
<figcaption>Unnest the xml list into wider form</figcaption>

### Unnest the list in each cell

```r
lp_df = lp_wider %>%
  # 1st time unnest to release the 2-dimension list?
  unnest(cols = names(.)) %>%
  # 2nd time to nest the single list in each cell?
  unnest(cols = names(.)) %>%
  # convert data type
  readr::type_convert() 
```

The data then has to be unnested two times. I do not quite understand why this is required though. Maybe because the values in the cells a in the form of "list in list"/"nested list"? Following are the results after `lp_wider` is passed through 1. the first unnest and 2. the second unnest. After the first unnest, each column is still a type of list with length of 1. The data are exposed only after the second unnest.

![](/post/2021-03-xml-dataframe-r/unnest-first-time.png)
<figcaption>tibble after unnest for the first time</figcaption>

![](/post/2021-03-xml-dataframe-r/unnest-second-time.png)
<figcaption>tibble after unnest for the second time</figcaption>

And finally, the xml is converted to a tidy tabular format for further analysis.

![](/post/2021-03-xml-dataframe-r/converted-tibble.png)
<figcaption>converted dataframe</figcaption>

---

## Other approaches

### Manual edit and conversion

The quick (though dumb) way to get the nested part of a XML is - manually delete the "outer" part! In the case of this resturant license XML, I only need the `<LPS>` part, and all other nodes (I am not sure about this is the correct terminology for XML) could be deleted. After that, I just need to use an onine [XML to CSV converter](https://www.convertcsv.com/xml-to-csv.htm) for the data format conversion.

### Using XML package

The **XML** package is an older package to transform xml to dataframes. 

https://blog.gtwang.org/r/r-xml-package-parsing-and-generating-xml-tutorial/

---

## References

https://community.rstudio.com/t/how-to-convert-a-partly-nested-xml-to-data-frame-using-xml2/36705/2

https://stackoverflow.com/questions/47254923/nested-xml-to-data-frame-in-r

https://megapteraphile.wordpress.com/2020/03/29/converting-xml-to-tibble-in-r/
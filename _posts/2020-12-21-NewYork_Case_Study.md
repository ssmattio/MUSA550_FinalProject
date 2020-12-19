---
title: "Case Study: New York State"
date: 2020-12-21
published: true
tags: [dataviz, folium]
excerpt: "Embedding interactive Folium charts on static pages using Jekyll."
altair-loader:
  altair-Site-Per-Pop: "charts/NY_NPS_Site_Per_Pop_altair.json"
  altair-Total-sites: "charts/NY_NPS_Site_Count_altair.json"
folium-loader:
  folium-chart-2: ["charts/percent_no_internet.html", "400"]
toc: true
toc_sticky: true
---

To drill down further into the analysis of NPS sites, New York was selected as a case study. New York
has one of the highest counts of NPS sites, making it an ideal case study.

## Distribution of NPS Sites in New York and Key Indicators

When analyzing the raw count of NPS sites, New York county exceeds all other counties with 499 sites. However,
these counts can be misleading when considering population density. With a population of over 1.6 million, New York County's
total number of listings per person is only 0.0003. Meanwhile, rural counties like Hamilton and Essex County have 0.004 and
0.002 listings per person. The interactive maps below compare these two metrics.

<div id="altair-Total-sites"></div><div id="altair-Site-Per-Pop"></div>



## Percentage of Households without Internet

<div id="folium-chart-2"></div>

See the [lecture 9B slides](https://musa-550-fall-2020.github.io/slides/lecture-9B.html) and the [lecture 10A slides](https://musa-550-fall-2020.github.io/slides/lecture-10A.html) for the code that produced these plots.

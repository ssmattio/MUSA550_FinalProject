---
title: "Case Study: New York State"
date: 2020-12-21
published: true
tags: [New York, hvplot, Machine Learning]
excerpt: "Applying the model at a more granular level"
altair-loader:
  altair-Site-Per-Pop: "charts/NY_NPS_Site_Per_Pop_altair.json"
  altair-Total-sites: "charts/NY_NPS_Site_Count_altair2.json"
  altair-map-panel1: "charts/NY_demographic_data_1.json"
  altair-map-panel2: "charts/NY_demographic_data_2.json"
toc: false
toc_sticky: false
---

To drill down further into the analysis of NPS sites, it is useful to apply the model at a smaller
scale. New York has one of the highest counts of NPS sites, making it an ideal case study to determine
the model's strength at both a national and local level.

## Distribution of NPS Sites in New York and Key Indicators

When analyzing the raw count of NPS sites, New York county exceeds all other counties with 499 sites. However,
these counts can be misleading when considering population density. With a population of over 1.6 million, New York County's
total number of listings per person is only 0.0003. Meanwhile, rural counties like Hamilton and Essex County have 0.004 and
0.002 listings per person. The maps below compare these two metrics.

<div id="altair-Total-sites"></div><div id="altair-Site-Per-Pop"></div>

The maps below show other demographic indicators that will be used in the regression. Areas with a higher percentage of the population
with a degree appear to align with counties with higher counts of NPS sites, as well as areas with a higher population.

<div id="altair-map-panel1"></div>

The second series of indicators show economic indicators. 

<div id="altair-map-panel2"></div>



## Applying the Random Forest Algorithm
The results below show the outcome of applying the model at a smaller scale.

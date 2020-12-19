---
title: "Cluster Analysis"
date: 2020-12-21
published: true
tags: [dataviz, matplotlib]
excerpt: "This is an example blog post that embeds a matplotlib image."
altair-loader:
  altair-chart-1: "charts/heatmap_culsters.json"
  altair-plot-1: "charts/plot1_clusters.json"
  altair-map-1: "charts/map1_clusters.json"
toc: false
toc_sticky: false
read_time: false
---

## KMeans Cluster Analysis

After reviewing the exploratory data and maps, we wish to identify clusters based on several census-based data we are importing into our dataset.
These added columns represent several assumptions that we wish to test:

## Added variables from the ACS

MISSING EXPL OF VARIABLES CREATION

MISSING VARIABLES TABLE -> TO BE CREATED WITH MATPLOTLIB?

## testing for autocorrelation

missing text 

<div id="altair-chart-1"></div>

missing text about pairs

## Initial Cluster analysis

We first test the merged data using five clusters, while scaling the different variables:

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

kmeans = KMeans(n_clusters=5)

NPS_census_scaled = scaler.fit_transform(NPS_census[['LISTINGS_PER_POP','GDP_2019_4Q','white_per','BelowPoverty_per','Above150_inc_per','ind_const_per']])

scaler = StandardScaler()

kmeans.fit(NPS_census_scaled)

NPS_census['label'] = kmeans.labels_

alt.renderers.enable('notebook')
```
The initial test leads to the dividion that is shown within this plot: 

<div id="altair-plot-1"></div>

Additional expl on plot...

when mapping these clusters:

<div id="altair-map-1"></div>

the distrb. of it?? MISSING

## Adjusting the number of clusters using the elbow method

an explanation of why

The graph of the first test

the code to get the value

## Adjusted Map of Clusters

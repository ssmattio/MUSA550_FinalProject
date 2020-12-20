---
title: "Cluster Analysis"
date: 2020-12-20
published: true
tags: [altair]
excerpt: "KMeans cluster analysis of NPS count per population, by state"
altair-loader:
  altair-chart-1: "charts/heatmap_culsters.json"
  altair-plot-1: "charts/plot1_clusters.json"
  altair-map-1: "charts/map1_clusters.json"
  altair-map-2: "charts/map2_clusters.json"
hv-loader:
  hv-chart-1: "charts/table_variables.html"
toc: false
toc_sticky: false
read_time: false
---

## KMeans Cluster Analysis

After reviewing the exploratory data and maps, we wish to identify clusters based on several census-based data we are importing into our dataset.
These added columns represent several assumptions that we wish to test:

## Added variables from the ACS

To the GDP variable that was added within the exploratory data part, we wish to add more variables that are census-based. 
These veriables were selected since we assum possible correlation between them and the count of listing per population. 
The variables are broad and cover race, income, and education. They are constructed from the original categories of the census:

* % White = percent of white population within the state
* % Unemployed = percent of unemployed from total in labor force
* % population with higher degree = accosiate degree *or higher* from voting age population
* % below poverty rate = HH income in the past 12 months below poverty rate 
* % high income = HH with income of 150,000 and higher from all HH

<div id="hv-chart-1"></div>

## Testing for autocorrelation

Now that we have both the count per population, the GDP and the census variables, we wish to test for autocorrelation between tha variables. We do so to avoid using too similar variables within our clustering analysis, with the threshold of .6 to guide us.

<div id="altair-chart-1"></div>

As seen, the unemployment and the poverty variables are highly correlated, as well as the higher incom with higher education. We will choose one of each pair to use in our clustering analysis.

## Initial Cluster analysis

We first test the merged data using five clusters, while scaling the different variables:

```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

kmeans = KMeans(n_clusters=5)

NPS_census_scaled = scaler.fit_transform(NPS_census[['LISTINGS_PER_POP','GDP_2019_4Q','white_per','BelowPoverty_per','Above150_inc_per']])

scaler = StandardScaler()

kmeans.fit(NPS_census_scaled)

NPS_census['label'] = kmeans.labels_

alt.renderers.enable('notebook')
```
The initial test leads to the dividion that is shown within this plot: 

<div id="altair-plot-1"></div>

The chart presents listings per population vs. the GDP of the last quarter of 2019. The color represents the five clusters that were created. 
We can see that when factoring the amount of population, the correlation appears to be negative. When reviewing only count vs. GDP, it display an opposit correlation.

when mapping these clusters:

<div id="altair-map-1"></div>

The distribution of states between clusters is unequal. There is only one state within the third group (District of Columbia), and three within the zero cluster.

## Adjusting the number of clusters using the elbow method

We started by randomally choosing five clusters, but it is possible that the optimal amount of clusters is smaller or higher than that.
So, we will try to identify the optimal amount and fit our clustering analysis again according to the result. 

```python
# Number of clusters to try out
n_clusters = list(range(2, 20))

# Run kmeans for each value of k
inertias = []
for k in n_clusters:

    # Initialize and run
    kmeans = KMeans(n_clusters=k)
    kmeans.fit(NPS_census_scaled)

    # Save the "inertia"
    inertias.append(kmeans.inertia_)

alt.renderers.enable('notebook')
```
![elbow-plot]({{ site.url }}{{ site.baseurl }}/charts/elbow.png)

It is hard to define the right 'elbow' in this graph, so instead of selecting manually, we will use an algorithm to identify the optinal number of clusters.

```python
from kneed import KneeLocator

# Initialize the knee algorithm
kn = KneeLocator(n_clusters, inertias, curve='convex', direction='decreasing')

# Print out the knee 
print(kn.knee)

alt.renderers.enable('notebook')
```
The algorithm result is seven. 

## Adjusted Map of Clusters

Using the optimal number of clusters, we are re-fitting the data and plotting the map:

<div id="altair-map-2"></div>

Altough the number of clusters increased, the District of Columbia is still within the smallest cluster (the only value within it). 
It is not suprising consider the high amount of population and monuments within it, that sets it apart from the rest. 

Since this clustering method does not account for spatial attributes, it is interesting to see where on one hand, neighboring states are within the same clusters, and on the other some clusters are spread throughout the US.

---
title: "Project Introduction"
date: 2020-12-21
categories:
  - blog
altair-loader:
  altair-chart-1: "charts/allC.json"
  altair-chart-2: "charts/outputC4.json"
  altair-chart-3: "charts/GDP_chart.json"
  altair-map: "charts/maps_intro.json"

tags:
  - Github Page
  - update
---

## NPS listings

The National Register of Historic Places is the US official built heritage preservation list. Authorized by the National Historic Preservation Act of 1966, the NRHP is part of a national program to identify, evaluate, and protect America's historic and archeological resources. As of January 2020, the dataset of NHRP listed properties contains 95,354 items, that are distributed throughout all the states. We wish to review the socio-economic, geographical and temporal trends regarding this growing list of heritage.

**SOURCES**

NPS public data: https://www.nps.gov/subjects/nationalregister/database-research.htm , 
https://public-nps.opendata.arcgis.com/datasets/nps-national-register-of-historic-places-locations,
The ACS

## Listings per state

The initial dataset includes 67,443 rows, when each row is a property of historic importance within the US. This dataset is of historic properties listed on the National Register of Historic Places, and was last updated in November 2020. Before exploring the data, we need to clean it and aggregate it by states. 

```python
NPS.Status.unique()

NPS['Status'].value_counts()

NPS = NPS[NPS['Status']!='Removed']

# remove NaNs
NPS = NPS[NPS['geometry'].isna() != True]

NPS_grped = NPS.groupby('State').count().reset_index()

```
After cleaning and grouping the initial data, we can now review the status per state, with three different measurement ways:

<div id="altair-chart-1"></div>

We can see that the count per area is schewed because of the District of Columbia. We will review it again, ommiting the District:

<div id="altair-chart-2"></div>

The three measurments provide a different results. When simply counting the number of listing, NY state is on top, but when factoring the population size and the area, NY shifts lower in the ranking, while places such as South Dacota (population) or District of Columbia and Rhode Island gain prominance. 
It is important to understand the difference. In later stages, we will work with the count per population and with the simple count to construct different models. While the count per area is important, we will not explore it further in the project. When reviewing the count per population, we need to keep in mind that states' population is a dynamic figure that changed dramatically over the years. While the listings are aggregated up to 2020, a further review of listings vs. population over time is recommended to future work. 

## Adding GDP variable

Adding the GDP and plotting : MISSING TEXT

<div id="altair-chart-3"></div>

missing expl.

## Exploratory maps of results

<div id="altair-map"></div>

Missing text about the map and the difference of choosing each for our dependetqprimary variable

## next steps

In the next links, we will create clusters of the dataset, as well as a regression model to try and predict the accumulative values. We will then zoom-in to review a county-scale of the count to NY, and test our regression model on this case-study.

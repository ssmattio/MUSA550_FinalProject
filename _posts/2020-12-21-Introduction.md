---
title: "Project Introduction"
date: 2020-12-21
categories:
  - blog
tags:
  - Github Page
  - update
---

## NPS listings

The National Register of Historic Places is the US official built heritage preservation list. Authorized by the National Historic Preservation Act of 1966, the NRHP is part of a national program to identify, evaluate, and protect America's historic and archeological resources. As of January 2020, the dataset of NHRP listed properties contains 95,354 items, that are distributed throughout all the states. We wish to review the socio-economic, geographical and temporal trends regarding this growing list of heritage.

SOURCES
NPS public data: https://www.nps.gov/subjects/nationalregister/database-research.htm , The ACS

## Listings per state

The initial dataset includes 67443 rows, when each row is a property of historic importance within the US. Before exploring the data, we need to clean it an aggregate it by states. 

```python
NPS.Status.unique()

NPS['Status'].value_counts()

NPS = NPS[NPS['Status']!='Removed']

# remove NaNs
NPS = NPS[NPS['geometry'].isna() != True]

NPS_grped = NPS.groupby('State').count().reset_index()

```
- count graph

- count per population graph

- count per area graph

## Adding GDP variable

Adding the GDP and plotting :

GRAPH MISSING

## Exploratory maps of results

MISSING MAPS

## next steps

Missing expl to the next posts, and how they are relate to this one.


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll.

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

---
title: "Regression Analysis"
date: 2020-12-21
published: true
tags: [dataviz, altair, hvplot, holoviews]
excerpt: "Embedding interactive charts on static pages using Jekyll."
altair-loader:
  altair-chart-1: "charts/measlesAltair.json"
  ilil-test-1: "charts/myOutputChart1.json"
hv-loader:
  hv-chart-1: "charts/measlesHvplot.html"
toc: true
toc_sticky: true
---

Finally, the data was used in regression analysis to predict the number of NPS sites based on
several indicators. This analysis uses the same dataset as the cluster analysis, which contains the
NPS data joined with census data.

## Selecting a Machine Learning Algorithm

For this analysis, Random Forest was used to avoid overfitting the model to our sample of points and
because combining multiple numeric estimators can lead to a better, more accurate model. This model predicts
the number of NPS sites in a state.


First the data was split 70/30 into training and test sets. Then, the indicators were checked for high
correlation.

![Correlation](charts/Regression_Correlation.jpg)

```python
import altair as alt
alt.renderers.enable('notebook')
```

## Random Forest Algorithm

this is an example of text

<div id="ilil-test-1"></div>

this is an example of text

## HvPlot Example

Lastly, the measles incidence produced using the HvPlot package:

<div id="hv-chart-1"></div>

## Notes

- See the [raw source code](https://raw.githubusercontent.com/MUSA-550-Fall-2020/github-pages-starter/master/_posts/2019-04-13-measles-charts.md) of this post for details on how these charts were embedded.
- See the [lecture 13A slides](https://github.com/MUSA-550-Fall-2020/week-13/blob/master/lecture-13A.ipynb) for the code that produced these plots.

**Important: When embedding charts, you will likely need to adjust the width/height of the charts before embedding them in the page so they fit nicely when embedded.**

---
title: "Regression Analysis"
date: 2020-12-21
published: true
tags: [dataviz, altair, hvplot, holoviews]
excerpt: "Embedding interactive charts on static pages using Jekyll."
altair-loader:
  altair-chart-1: "charts/heatmap_culsters.json"
hv-loader:
  hv-chart-1: "charts/Importance_Chart.html"
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


First the data was split 70/30 into training and test sets. Then, the indicators were checked for autocorrelation.
As seen below, unemployment and poverty variables are highly correlated.

<div id="altair-chart-1"></div>

Then, a baseline was established with a linear regression model using the code below.

```python
# Linear model pipeline with two steps
linear_pipe = make_pipeline(StandardScaler(), LinearRegression())

# Fit the pipeline
print("Linear regression")
linear_pipe.fit(X_train, y_train)
```

The resulting training score is 0.755 and the resulting test score is 0.648. With this baseline
established, the random forest model pipeline can now be created.

```python
# Make a random forest pipeline
forest_pipeline = make_pipeline(
    StandardScaler(), RandomForestRegressor(n_estimators=100, random_state=42)
)

# Run the 10-fold cross validation
scores = cross_val_score(
    forest_pipeline,
    X_train,
    y_train,
    cv=10,
)
```
When the model is fit on the training data, the resulting score is -0.437. To better understand which features
are most important in the model,

<div id="hv-chart-1"></div>

## Testing the Model



## Results

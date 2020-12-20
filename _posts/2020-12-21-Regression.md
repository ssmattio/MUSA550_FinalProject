---
title: "Regression Analysis"
date: 2020-12-21
published: true
tags: [Machine Learning, altair, hvplot, Random Forest]
excerpt: "Predicting the amount of NPS sites with machine learning."
altair-loader:
  altair-chart-1: "charts/heatmap_culsters.json"
hv-loader:
  hv-chart-1: "charts/Importance_Chart.html"
toc: false
toc_sticky: false
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

The resulting test score is 0.1042. With this (low) baseline established, the
random forest model pipeline can now be created.

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
When the model is fit on the training data, the resulting score is 0.3947. This score is much stronger
than the baseline score, indicating that the model is a better fit. To better understand which features
are the strongest and most important to the model, they are then plotted and ranked by importance. By far, the strongest indicator
for predicting the amount of NPS sites is population, followed by percent of population at the highest income level.
This indicates that states with higher income and a higher amount of people are more likely to have a higher amount
of NPS sites, while low-income, low-population states are likely to have fewer sites. Given that the states with the
highest amount of NPS sites are California and New York, the model appears to be predicting accurately.

<div id="hv-chart-1"></div>



## Results
The map below shows the actual count of NPS sites by state, compared to the predicted values of the model. 

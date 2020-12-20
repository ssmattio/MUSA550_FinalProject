---
title: "Regression Analysis"
date: 2020-12-20
published: true
tags: [Machine Learning, altair, hvplot, Random Forest]
excerpt: "Predicting the amount of NPS sites with machine learning."
altair-loader:
  altair-chart-1: "charts/heatmap_culsters.json"
  altair-chart-2: "charts/Predicted_vs_Actual_map.json"
  altair-chart-3: "charts/Percent_Error.json"
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

# making predictions:
model_name = "randomforestregressor"
param_grid = {
    f"{model_name}__n_estimators": [5, 10, 15, 20, 30],
    f"{model_name}__max_depth": [None, 2, 5, 7, 9, 13],
}

# Create the grid and use 5-fold CV
grid = GridSearchCV(pipe, param_grid, cv=5)

# Run the search
grid.fit(train_set, y_train);
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

<div id="altair-chart-2"></div>

The maps above shows the actual count of NPS sites by state, compared to the predicted values of the model. The model predicts well
for most states, except Arkansas, Ohio, and Massachusetts. In these cases, the model overpredicted the count, predicting site counts
that were higher than the actual counts.

Next, the percent error of each state is mapped out. The distribution of high errors shows that the model is better at predicting states
with a higher population and population density. States like Nevada, Arkansas, Montana, and Ohio had much larger errors.

<div id="altair-chart-3"></div>

## Next Steps
Now that the model has been applied at a national scale, it can be tested at a more local level with state data. The next page provides
a case study using the model for New York state.

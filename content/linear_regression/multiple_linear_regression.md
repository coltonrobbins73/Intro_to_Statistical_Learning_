+++
title = 'Multiple Linear Regression'
date = 2024-04-11T14:50:25-07:00
draft = false
weight = 4
+++

Simple linear regression is a powerful statistical tool but in most contexts, many predictors are used to estimate a response variable. To more accurately model these scenarios, we must use multiple linear regression where each predictor is multiplied against an unknown regression coefficient {{<math>}}$\beta${{</math>}} as in this equation form :

{{<math>}}$$y=\beta_0+\beta_1X_1+\beta_2X_2....+\beta_pX_p$${{</math>}}

To fit a model using multiple predictors, we use the same residual sum of squares strategy (RSS) similar to simple linear regression. The derived equations that minimize RSS for multiple linear regression are beyond the scope of this text, but we can still use computational software to estimate the regression coefficients and plot them in the graph below. Note for this example we have two predictors, so we are fitting a plane to the data. If we had more than two predictors, we would fit a hyperplane to the data.

![RSS Example for Two Predictors](/intro_to_statistical_learning/images/RSS_multi_predictor.jpg)

### Predictor correlation considerations

Sometimes simple linear regression can show a high-confidence relationship between a predictor and response variable but when that same predictor is included in a multiple linear regression, that relationship is no longer credible. This occurs when there is a correlation between predictor variables. When a non-informative predictor is correlated with a true informative predictor, the non-informative predictor gets credit for the predictive power of its correlative partner. However, when these predictors are considered together in a single multivariable equation, the influence of each individual variable is properly modeled and can be isolated.

### Hypothesis testing for multiple linear regression

For multiple linear regression the hypothesis test is computed using the ***F*** statistic :

{{<math>}}$$F = \frac{(TSS - RSS)/p}{RSS/(n-p-1)}$${{</math>}}

The F test essentially compares the total error from 2 models

1. A fit line without coefficient values for any of the predictors.
2. A fit line with estimated coefficients for each predictor.

This is represented in the F test equation as the error difference between the two models (numerator) over the error of just the predicted model (denominator). When RSS is much smaller than TSS, you will get a large F statistic value  The alternative is that both the numerator and denominator approximate {{<math>}}$\sigma ^2${{</math>}} and thus the F statistic approaches 1. Rejection of the null hypothesis depends on the values of ***F***, ***n***, and ***p***. If these values are sufficiently large, we can reject the null hypothesis and claim that at least one of the predictors is useful for calculating the response variable.

### Isolating contributing variables

Using the F statistic we can determine if at least one of the predictors is related to the response, but practically speaking there will likely be only a subset of predictors that is truly useful for our model. **Variable selection** is used in this context and can be approached in three different ways :

1. **Forward selection** : we start with a null model that contains only an intercept and then separately fit ***p*** simple linear regression lines to the data. The model with the lowest RSS is then combined with all other predictors to generate a new two-variable model with the lowest RSS. The chain is increased in this fashion until some stopping rule is reached.
2. **Backward selection** : we start with a model containing all predictors and then remove the variable with the largest p-value. A new model is generated and once again the variable with the largest p-value is removed.
3. **Mixed selection** : we start with a null model and add variables iteratively just as in forward selection. However, if any of the new additions have a sufficiently high p-value, those variables are skipped until a model is fully built with sufficiently low p-values.

### Evaluating model fit

Multiple linear regression uses the same evaluation techniques as simple linear regression (RSE and {{<math>}}$R^2${{</math>}}). However, it is important to note that adding more variables to our model will decrease RSS and therefore increase {{<math>}}$R^2${{</math>}}. However, if the increase in {{<math>}}$R^2${{</math>}} from adding a specific variable is not substantial it indicates that we are simply overfitting to the training data and the gains in RSS are simply due to coincident random noise. Oftentimes, these situations lead to an increase in RSE given by the formula :

{{<math>}}$$RSE=\sqrt{\frac{1}{n-p-1}RSS}$${{</math>}}

In this equation, if the reduction in RSS from adding a new variable is minor, it will not be able to overcome the increase in ***p*** and thus RSE will be large.

### Confidence and prediction intervals

The most important concept to remember here is that prediction intervals will always be larger than confidence intervals and, in general, you want to be using prediction intervals in practical situations. The confidence interval relates to our confidence for the already recorded data whereas the prediction interval is for predicting new data in the future. The confidence interval only considers the reducible error of our equation in estimating the population parameter. In other words, we will always encounter a sampling bias in our data that imputes uncertainty into our estimate of the population average. The prediction interval considers both the reducible and irreducible error of the model.


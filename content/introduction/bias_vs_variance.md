+++
title = 'Bias vs Variance'
date = 2024-04-10T11:56:59-07:00
draft = false
weight = 3 
+++

Bias and variance both refer to the degree of error of a particular model. However, bias refers to training error whereas variance refers to testing error. As we will see the relationship between these two measurements has profound consequences for statistical learning.

### Assessing performance

Different statistical methods perform better under different circumstances. To identify the best one for a particular use case, it is important to have an empirical method for evaluating model performance. For regression, mean squared error is typically used:

{{<math>}}$$MSE = 1/n \sum_{i=1}^n (y_i - f(x_i))^2$${{</math>}}

Where {{<math>}}$f(x_i)${{</math>}} is the predicted function output for the ith observation. In essence, we are just taking the difference between true ***y*** and predicted ***y*** and dividing it by the total number of observations. When our prediction is accurate, the two vectors will be nearly identical and the MSE will be low.

### Training MSE vs Test MSE

MSE can be and should be conducted for both training data that has been processed by our algorithm and testing data that the algorithm has never seen. 

![Train MSE vs. Test MSE](/intro_to_statistical_learning/images/testMSE_vs_trainMSE.jpg)

Here we have 3 different approximations of ***f*** :

1. **Linear regression line (orange)** : poor fit to the curved data distribution produces a high train and test MSE.
2. **Smoothing splines (blue)** : good fit to the curved data produces low train and test MSE.
3. **Smoothing splines (green)** : over fit to the noise of the data produces very low train MSE but high test MSE.

As you can see, when the statistical model becomes too flexible, the fit becomes too sensitive to the noise of the training data and therefore cannot generalize well to new situations in the test data. In practice, ***f*** can never be truly known, so we are unable to attain explicit graphs for MSE, bias, and variance but these concepts should be considered when designing a statistical model.
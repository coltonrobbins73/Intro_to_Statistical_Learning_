+++
title = 'Simple Linear Regression'
date = 2024-04-10T15:05:20-07:00
draft = false
weight = 3
+++

Linear regression is one of the simplest models for estimating a response. A standard linear equation takes this form :

{{<math>}}$$Y = \beta _0 + \beta _1 X$${{</math>}}

Where {{<math>}}$\beta _0${{</math>}} is the y-intercept when {{<math>}}$x_0 = 0${{</math>}} and {{<math>}}$\beta _1${{</math>}} is the slope of the line. Simple linear regression accounts for only 1 parameter and thus we only need to calculate 2 coefficients {{<math>}}$(\beta)${{</math>}} for the intercept and the slope.

### Residual sum of squares

To compare linear fit, we need a numerical equation to score different predicted coefficient values. This is commonly accomplished with **residual sum of squares** (RSS) where each observed value is compared 

![RSS Example](/Intro_to_Statistical_Learning/images/RSS_example.jpg)

### Derivation of residual sum of squares

Instead of approximating the best fit line and then iteratively improving on it, we can use the derivative of the RSS formula to find the global minima where the slope of the change in the RSS is equal to 0. [Click here](https://www.youtube.com/watch?v=ewnc1cXJmGA&ab_channel=jbstatistics) for a wonderful explanation on how to derive these formulas.

For simple linear regression, we have two coefficients to calculate (the slope and the intercept) and so we can combine the two derivations to find the global maximum shared by both values as demonstrated in these graphs.

![Least squares minima](/Intro_to_Statistical_Learning/images/least_squares_minima.jpg)

### Residual standard error

Now that we have the best-fit line for our data, we need to quantify how well we have modeled the relationship between our input and output variables. Despite maximizing the score of our best-fit line, we will always retain an unexplained error term {{<math>}}$\epsilon${{</math>}} that represents random variations in the data that our model did not capture. **Standard error** is used to quantify the uncertainty in our prediction for each parameter (slope and intercept).

{{<math>}}$$Standard \ error \ intercept= \beta _0^2 = \sigma ^2\frac{1}{n}+\frac{\bar{x}^2}{\sum _i^n (x_i-\bar{x})^2}$${{</math>}}

{{<math>}}$$Standard \ error \ slope= \beta _1^2 = \frac{\sigma ^2} {\sum _i^n (x_i-\bar{x})^2}$${{</math>}}

 Here we see that as the spread of ***x*** increases in the denominator, the standard error decreases because we have more leverage for estimating the best-fit line if we have a more evenly distributed data set. In other words, if all the data was concentrated around the mean, the best-fit line would likely fluctuate. Furthermore, as ***n*** increases we gain more confidence in the model and again reduce our standard error.
 
 In the standard error formulas, {{<math>}}$\sigma ^2 = Variance(\epsilon)${{</math>}} which is also known as **residual standard error** (RSE) or the standard deviation of error terms {{<math>}}$\epsilon${{</math>}} for all observations. For this formula to be accurate, each error term {{<math>}}$\epsilon${{</math>}} needs to have a common variance. This is not the case in practice as can be seen in figure 3.1 where the residuals of observations to the left seem to have a tighter distribution than the residuals of the observations on the right of the plot. However, despite this practical discrepancy, we can still reasonably approximate RSE using this formula :

{{<math>}}$$RSE = \sqrt{RSS/(n-2)}$${{</math>}}

Using this equation on our dating from Figure 3.1, we produce an RSE of 3.26 which means that even under a perfect prediction model we can expect that our accuracy will be off by about 3,260 units. The mean observation is 14,000 which equates to a percentage error of 23%. 

### {{<math>}}$R^2${{</math>}} statistic

RSE measures the deviation of the fitted line but the units are relative to the specific problem we are working on. However, {{<math>}}$R^2${{</math>}} provides this information as a proportion equal to between 0 and 1 using this formula :

{{<math>}}$$R^2=\frac{TSS-RSS}{TSS}$${{</math>}}

Where TSS = total sum of squares and uses the same equation as RSS but the line in question is a horizontal line at the mean position of ***y***. In other words, our predicted fit line is compared against the absolute worst possible fit line to determine the overall reduction in variance. The worst possible fit line is a horizontal line located at the mean of the data. A horizontal line fit indicates no relationship between the predictor and the response variables and the distance from this line to each data point (aka the **residuals**)represents the total variance of the data distribution. When we fit a new line to the data, we can measure the new residuals and compare the summed average to the summed average of the worst fit line. If the summed average of residuals is lower in the new fit line, we can show that a portion of the variance can be explained by the relationship between the predictor and response variables. The ratio of this improvement is the {{<math>}}$R^2${{</math>}} value.

### Confidence intervals

Standard errors are used to equate model-specific parameter units with standard deviations. In Figure 3.1, we see that each unit on the y-axis is reported as 1,000 items sold and each unit on the x-axis is reported as 1,000 dollars invested. Two standard deviations from a normal distribution encapsulates 95% of the data, so we can multiply our standard error by 2 to retrieve the practical values in our confidence interval. For example, if our standard error for the slope {{<math>}}$SE\beta _1 = 2.75${{</math>}} then we can claim that for every 1,000 dollars invested, we will increase sales by 47.5 units +/- 5.5 units.

### Hypothesis testing

Now that we have calculated the standard error for our parameters, we can use these values to conduct a hypothesis test for the relationship between input and output variables. In regards to the slope of a line, the null hypothesis is that there is no relationship between a predictor and a response variable so the slope is 0. Thus, when we estimate a slope that is far from 0, we can be more confident that there is a true relationship between the variables, assuming the standard error is sufficiently low. When the standard error is high, we must observe a high slope value to reject the null hypothesis. Alternatively, when the standard error is low, we do not need such a high slope value to be confident in the relationship between variables. In practice, we would compute a t-statistic to determine the likelihood that our observations are due solely to chance.

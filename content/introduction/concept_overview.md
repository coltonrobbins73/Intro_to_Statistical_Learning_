+++
title = 'Statistical Learning Methods'
date = 2024-04-07T10:37:06-07:00
draft = false
weight = 2
+++

Imagine a large matrix **X** where rows are observations (***n***) and columns are features (***p***). There exists a distinct yet unknown function (***f***) with which any row ({{<math>}}$x_{i}^{T}${{</math>}}) can be used to derive the corresponding output ({{<math>}}$y_{i}${{</math>}}). In other words, you take an input matrix and apply a function to yield an output vector. Statistical learning essentially works to approximate ***f*** as closely as possible.

### Major goals of function estimation

1. **Prediction** : estimating the output state of a system given a set of input variables. With prediction, we care only about the accuracy of predicted outcomes and do not necessarily worry about how ***f*** works. An example of this is whether or not a medical drug works.

2. **Inference** : understanding the underlying relationship between a set of input variables and output variables. With inference, we want to understand how each predictor is associated with the output variables. An example of this is how advertising strategies affect sales.

### Statistical methods for finding ***f***

##### Parametric methods

Refers to a category of methods that relies on assumptions about the form of ***f***.

To use a parametric method :

1. Select a pre-defined model such as the *linear model* : {{<math>}}$y=\beta_0+\beta_1X_1+\beta_2X_2....+\beta_pX_p${{</math>}}

2. Use training data to fit the model and thereby estimate all the coefficients ***B***.

 This process reduces the complexity of estimating ***f*** entirely where instead you only need to estimate a series of parameters that relates input and output data. The simplicity of parametric methods makes calculation and interpretation much easier. However, the downside of parametric methods is that they can be too rigid to accurately model complex phenomenon. Moreover, if the initial model is poorly chosen, our estimate of ***f*** will never approach its true form.

##### Non-parametric methods

Refers to a category of methods that do not rely on assumptions about the form of ***f***. These methods aim to fit an estimate of ***f*** based purely on the data present in the training set. Smoothing splines, is an example of a non-parametric method where function forms are fit around each data point and then smoothed across adjacent points. Due to the flexibility of these methods, a more exact estimate can usually be attained when compared to parametric methods. However, the major drawback to using non-parametric methods is that they require large amounts of data to adequately capture the form of ***f***. Since no assumptions are being made about ***f***, these methods require complete, continuous, and plentiful data to cover the full range of ***f***.

### Accuracy vs interpretation

Statistical methods lie on a continuum of flexibility which has a direct impact on interpretability. The more rigid a method is the easier it is to interpret. In other words, when a model becomes more complex, it is harder to understand the relationships between all the components of that model. Therefore in some circumstances, it is preferable to use a simple interpretable model. In fact, sometimes a more rigid model is more accurate due to the phenomenon of overfitting.

![Flexibility vs Interpretability](/intro_to_statistical_learning/images/flexibility_vs_interpretability.jpg)

### Supervised vs unsupervised learning

**Supervised** : relies on pre-labeled data to estimate the relationship between predictors and responses. Linear regression, logistic regression, and support vector machines are just some examples of this strategy.

**Unsupervised** : uncovers hidden relationships between variables without any ground truth information. This is arguably the more challenging category of statistical learning because patterns in the data must be inferred indirectly. An example of this method is clustering analysis where classification boundaries are formed based on the arrangement of similar data points that are called clusters.


+++
title = 'Classification'
date = 2024-04-10T12:25:09-07:00
draft = false
weight = 4
+++

Classification refers to a qualitative output given a specific set of inputs and follows comparable concepts to regression-based methods. Thus, the error rate for classification methods can be expressed as such:

{{<math>}}$$MSE = 1/n \sum_{i=1}^n I(y_i \neq f(x_i))$${{</math>}}
`
Where ***I*** is an indicator variable that equals 1 if the predicted differs from the actual value and 0 if the prediction follows the actual value. 

### Bayes error rate

Bayes' theorem is simply the idea of modulating prior information with new information. An example would be given the **prior** ratio of the total numbers of class A and class B and the **new** information of input values ***X***, where should the new output be classified? This idea may seem simple but has profound implications for data science in that we can quantify changing probabilities with respect to incoming information.

For classification models, the theoretical lowest possible error rate is called the ***Bayes error rate*** aka the irreducible error rate : 

{{<math>}}$$Bayes\ error\ rate = 1- E(max_j Pr(Y=j | X))$${{</math>}}

Where E is the expected mean value of probabilities for all values of ***X***. Essentially, we are saying that given a perfect boundary drawn between categories, the combined uncertainty for all values of input ***X*** is equal to the Bayes error rate.

![Bayes classification boundary](/Intro_to_Statistical_Learning/images/bayes_classification.jpg)

For this example, the blue and orange populations overlap, so within this region, there is some inherent uncertainty about which class should be identified. If you combine all uncertainty for this model, you get the optimal error rate of 0.133.

### K-nearest neighbors

KNN classifiers identify the ***K*** number of points closest to a new input value {{<math>}}$x_0${{</math>}} and assigns a classification to that point based on the class of the average of the closest neighbors.

{{<math>}}$$KNN\ Classifier = Pr(Y=j | X) = 1/K \sum_{i \epsilon N_0} I(y_i = j)$${{</math>}}

Where {{<math>}}$N_0${{</math>}} is a subset of points that are within the defined nearest neighbor range to the test point {{<math>}}$x_0${{</math>}}.

![KNN K choice](/Intro_to_Statistical_Learning/images/KNN_K_choice.jpg)

As you can see, the choice of ***K*** has a profound effect on the flexibility of the boundary fit for this classifier. When larger numbers of ***K*** are chosen, the boundary becomes more general and less sensitive to noise. In practice, a robust but intermediate value of K is often chosen and must be verified using error rates often through several iterations.
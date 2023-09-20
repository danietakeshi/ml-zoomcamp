# Understanding Linear Regression in Machine Learning

Welcome to lesson five of machine learning in ZoomCamp, session two. In this lesson, we will delve into the fundamentals of linear regression—a foundational model for solving regression problems in machine learning, where the goal is to predict numerical values. Recall that in machine learning, we have three main problem types: regression, classification, and ranking. Today, we are focusing on regression, and more specifically, linear regression.

## Linear Regression Basics

Linear regression is a supervised learning algorithm used for predicting a continuous output, typically referred to as the target variable. In the context of linear regression, we have a feature matrix, often denoted as `X`, and a target variable, denoted as `Y`. The goal is to establish a linear relationship between the features and the target variable.

In its simplest form, linear regression can be expressed by the following equation:

\[Y = G(X)\]

- \(Y\) represents the target variable (in this case, the price we want to predict).
- \(G\) is our linear regression model.
- \(X\) denotes the feature matrix containing various features of the data.

Before diving into the details, let's consider a simplified example where we focus on a single observation, a car, and its corresponding features.

## Single Observation Example

Imagine we are dealing with one specific car and its attributes. Each feature of the car, such as engine horsepower, miles per gallon in the city, and popularity, can be represented as a vector. This vector, denoted as \(X_i\), contains \(n\) elements, where each element corresponds to a different characteristic of the car.

Here's what this \(X_i\) vector might look like:

\[X_i = [X_{i1}, X_{i2}, \ldots, X_{iN}]\]

- \(X_{i1}\) represents the engine horsepower.
- \(X_{i2}\) represents the miles per gallon in the city.
- \(X_{iN}\) represents the popularity of the car.

Our goal is to build a function that takes all these features (\(X_{i1}\) to \(X_{iN}\)) as input and produces a prediction that is close to the car's price (\(Y\)). In mathematical terms, this function can be represented as:

\[Y_i = G(X_i)\]

Now, let's examine a specific example:

- Engine Horsepower (\(X_{i1}\)): 453
- Miles Per Gallon in the City (\(X_{i2}\)): 11
- Popularity (\(X_{iN}\)): 86

For this particular car, \(X_i\) would look like this:

\[X_i = [453, 11, 86]\]

To calculate the predicted price (\(Y_i\)) for this car, we need to determine the weights associated with each feature and a bias term. The formula for linear regression can be expressed as follows:

\[Y_i = w_0 + \sum_{j=1}^{N} w_j X_{ij}\]

- \(w_0\) is the bias term.
- \(w_j\) represents the weight associated with feature \(X_{ij}\).
- \(N\) is the number of features.

In this formula, we calculate the weighted sum of all features and add the bias term to obtain our prediction (\(Y_i\)). Now, let's see how we can implement this in code.

## Implementing Linear Regression

To implement linear regression in code, we'll start with a simple Python function. We'll denote this function as `linear_regression`. Here's a sample implementation:

```python
import numpy as np

def linear_regression(X_i, weights, bias):
    prediction = bias
    for j in range(len(X_i)):
        prediction += weights[j] * X_i[j]
    return prediction
```

In this code:
- `X_i` is the feature vector for the specific car.
- `weights` is a vector containing the weights associated with each feature.
- `bias` is the bias term.

The `linear_regression` function calculates the predicted price for the car using the linear regression formula we discussed earlier.

## Making Predictions

Let's see how this function works with our example car:

```python
# Example feature vector for the car
X_i = [453, 11, 86]

# Example weights and bias (you'll learn how to determine these weights later)
weights = [0.01, 0.04, 0.002]
bias = 7.17

# Calculate the predicted price using linear regression
predicted_price = linear_regression(X_i, weights, bias)
print("Predicted Price:", predicted_price)
```

In this example, we have provided weights and a bias term, which are arbitrary values for demonstration purposes. The output will be the predicted price for the car based on the features and weights we provided.

## Understanding the Predictions

Let's break down the prediction process:

1. We start with the bias term (\(w_0\)), which represents the initial prediction if we know nothing about the car. In our case, it

's set to 7.17.

2. We iterate through each feature in the feature vector (\(X_i\)) and multiply it by the corresponding weight. The weights determine how much influence each feature has on the prediction. These weights are learned from the data during the training phase.

3. We sum up all these weighted feature values and add the bias term to obtain the final prediction (\(Y_i\)).

In practice, we don't set the weights and bias manually; instead, we use training data to learn the optimal values for these parameters. This process is called **training the linear regression model**.

## Key Takeaways

In this lesson, we introduced the basics of linear regression, which is a fundamental algorithm in machine learning for solving regression problems. We discussed the key components of linear regression, including the feature matrix (\(X\)), target variable (\(Y\)), weights, and bias term. We also provided a simple Python implementation of linear regression and explained how to make predictions using this model.

In the next lesson, we will dive deeper into how to train a linear regression model and determine the optimal weights and bias. Stay tuned for a more detailed exploration of this crucial aspect of linear regression.
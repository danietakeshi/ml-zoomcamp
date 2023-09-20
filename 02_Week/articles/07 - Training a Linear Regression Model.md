# Training a Linear Regression Model

In this article, we will discuss the process of training a linear regression model from scratch using the normal equation method. We will also provide code snippets from a Jupyter Notebook to demonstrate the implementation step by step.

## Introduction

Linear regression is a fundamental machine learning algorithm used for predicting a continuous target variable based on one or more input features. To make accurate predictions, we need to find the optimal weights (coefficients) for each feature. In this article, we will walk through the process of training a linear regression model using the normal equation.

## Transcription

Before we dive into the implementation, let's review the key concepts mentioned in the transcription:

- We have a feature matrix denoted as `X` and a target vector `Y`.
- Our goal is to find the weights vector `W` such that `X * W` approximates `Y`.
- We discussed the issue of finding an exact solution to the system and how it's not always possible, especially when `X` is not square.
- To find an approximate solution, we introduced the Gram matrix `XTX`, which is the product of the transpose of `X` and `X`.
- We mentioned that `XTX` is usually a square matrix, allowing us to find its inverse.
- The formula to calculate the weights `W` is `W = (XTX)^(-1) * XT * Y`.

## Implementation

Let's implement the training process step by step using Python code snippets in a Jupyter Notebook. We'll start with creating the Gram matrix, finding its inverse, and then calculating the weights `W`.

```python
import numpy as np

# Create a sample feature matrix X
X = np.array([
    [1, 2, 3],
    [1, 3, 4],
    [1, 4, 5],
    [1, 5, 6],
    [1, 6, 7]
])

# Create a sample target vector Y
Y = np.array([10, 12, 14, 16, 18])

# Calculate the Gram matrix (XTX)
XTX = np.dot(X.T, X)

# Find the inverse of XTX
XTX_INV = np.linalg.inv(XTX)

# Calculate the weights (W)
W = np.dot(np.dot(XTX_INV, X.T), Y)

# Split W into bias (W[0]) and coefficients (W[1:])
bias = W[0]
coefficients = W[1:]

print("Bias (Intercept):", bias)
print("Coefficients:", coefficients)
```

In the code above:

- We create a sample feature matrix `X`, where the first column is composed of ones (for the bias term), and a sample target vector `Y`.
- We calculate the Gram matrix `XTX` by taking the dot product of the transpose of `X` and `X`.
- We find the inverse of `XTX` using NumPy's `np.linalg.inv` method.
- Finally, we calculate the weights `W` by applying the normal equation formula.

## Conclusion

Training a linear regression model involves finding the optimal weights that minimize the difference between the predicted values and the actual target values. The normal equation method provides a straightforward way to compute these weights. In this article, we have provided code snippets within a Jupyter Notebook environment to demonstrate the step-by-step implementation of this process. By understanding the normal equation, you can apply linear regression to various real-world regression problems.

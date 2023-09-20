# Understanding Linear Regression in Vector Form

Welcome to lesson six of session two of the Machine Learning ZoomCamp! In this lesson, we will explore linear regression in vector form. So far, we've discussed linear regression for individual data points. Now, we'll generalize our understanding to handle multiple data points simultaneously using matrices.

## Recap: Linear Regression for a Single Data Point

Previously, we discussed linear regression for a single data point, focusing on predicting the price of a car. We used the following equation:

\[Y_i = w_0 + \sum_{j=1}^{N} w_j X_{ij}\]

- \(Y_i\) represents the predicted price for the car.
- \(w_0\) is the bias term.
- \(w_j\) represents the weight associated with feature \(X_{ij}\).
- \(N\) is the number of features.

Now, let's examine how we can generalize this for multiple data points.

## Vector Form of Linear Regression

### Dot Product Simplification

First, let's consider the dot product operation in our equation:

\[Y_i = w_0 + \sum_{j=1}^{N} w_j X_{ij}\]

This dot product operation can be simplified as:

\[Y_i = \mathbf{X}_i \cdot \mathbf{w}\]

Here,
- \(\mathbf{X}_i\) represents the feature vector for a specific car.
- \(\mathbf{w}\) represents the weight vector.

We've simplified the prediction process using dot products, making our code more concise and intuitive.

### Adding a Virtual Feature

Next, we'll introduce a virtual feature, \(X_{i0}\), which is always set to 1 for each data point. This virtual feature represents the bias term. By doing this, we can simplify our equation further:

\[Y_i = \mathbf{X}_i \cdot \mathbf{w}\]

Our weight vector (\(\mathbf{w}\)) will now have one extra element, \(w_0\), which corresponds to this virtual feature. This allows us to use matrix-vector multiplication for the entire linear regression.

### Generalization for Multiple Data Points

Now, let's think about all the examples in our dataset, not just one car. We have a feature matrix, \(\mathbf{X}\), which contains all the data points. In this matrix:

- We have rows corresponding to different data points (e.g., cars).
- For each row, we have the features.
- We prepend a column of ones to represent the virtual feature for bias.

For example, if we have \(m\) data points (cars) and \(n\) features, our feature matrix \(\mathbf{X}\) will be of size \(m \times (n + 1)\).

### Matrix-Vector Multiplication

To apply linear regression to multiple data points, we need to perform matrix-vector multiplication. We take our feature matrix \(\mathbf{X}\) and our weight vector \(\mathbf{w}\), and we multiply them together. The result is our predictions for all the data points simultaneously.

## Implementation Example

Now, let's see how this works in code using Python. We have three cars as examples:

```python
x1 = [1, 148, 24, 1385]
x2 = [1, 132, 25, 2031]
x10 = [1, 453, 11, 86]

X = [x1, x2, x10]
```

We create our feature matrix `X` by appending the virtual feature to each feature vector. Then, we have our weight vector `w_new`, which includes the bias term.

```python
X = np.array(X)
X.dot(w_new)
```

Using matrix-vector multiplication, we obtain the predictions for all three cars at once.

## Conclusion

In this lesson, we generalized linear regression to handle multiple data points simultaneously by using matrices. We started by simplifying the equation using dot products and then introduced a virtual feature for the bias term. This allowed us to perform matrix-vector multiplication to make predictions for an entire dataset at once.

You might be wondering how to determine the values of the weights (\(w_0, w_1, \ldots, w_n\)). We'll address this in the next lesson, where we discuss the process of training a linear regression model to find the optimal weights from data. Stay tuned for more insights into this essential aspect of linear regression!
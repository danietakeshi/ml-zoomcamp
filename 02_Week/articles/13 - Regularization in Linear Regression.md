# Understanding Regularization in Linear Regression

Welcome back to Lesson 13 of Machine Learning in ZoomCamp Session 2! In this lesson, we'll dive into the topic of regularization. In the previous lesson, we worked on handling categorical variables in our dataset. Now, let's explore regularization techniques and their importance in linear regression.

## Recap: Handling Categorical Variables

Before we jump into regularization, let's briefly recap what we've done in the previous lesson. We added categorical variables to our dataset and implemented code to handle these variables in our `prepare_X` function. While preparing the feature matrix `X`, we faced a problem: a very high root-mean-square error (RMSE) and unusually high weights in our linear regression model.

## The Problem: Singular Matrix

The root of our problem lies in the matrix operations performed in linear regression. When we use the normal equation to train our model, we encounter the following operation:

![Normal Equation](images/normal_equation.png)

The issue arises with this part: taking the inverse of the Gram matrix (XTX). Sometimes, this inverse doesn't exist. It typically occurs when our feature matrix X has duplicate features or columns. In linear algebra, this means that one column can be expressed as a linear combination of other columns. Let's demonstrate this problem:

```python
X = [
    [4, 4, 4],
    [3, 5, 5],
    [5, 1, 1.00001],
    [5, 4, 4],
    [7, 5, 5],
    [4, 5, 5.00000001],
]
```

Notice that the second and third columns have almost identical values, making the third column a duplicate of the second. When we attempt to calculate the inverse of XTX, we encounter an error: "Matrix is singular."

## Noise and Regularization

Real-world data isn't always clean, and noise can introduce tiny variations in our data. For example, instead of recording a value as exactly 5, it might be recorded as 5.0001. These small variations can prevent XTX from being a singular matrix, and inverses can be calculated. However, the resulting weights can become extremely large, causing issues in our model.

## Regularization to the Rescue

To address this problem, we use a technique called **regularization**. The key idea is to add a small number (usually denoted as α or λ) to the diagonal of the Gram matrix XTX. This small addition helps control the weights, ensuring they don't grow too large.

![Regularization](images/regularization.png)

By adjusting the value of α, we control the degree of regularization. Larger α values result in more significant regularization and smaller weight values.

Let's illustrate this with a smaller example:

```python
XTX = [
    [1.01, 2, 2],
    [2, 1.01, 1.000001],
    [2, 1.000001, 1.01],
]
```

Initially, this matrix causes the same "Matrix is singular" error. However, by adding α to the diagonal, we make the matrix invertible:

```python
XTX = XTX + 0.01 * np.eye(3)
```

## Implementing Regularization

Now, let's implement regularization in our linear regression model:

```python
def train_linear_regression_reg(X, y, r=0.001):
    ones = np.ones(X.shape[0])
    X = np.column_stack([ones, X])
    
    XTX = X.T.dot(X)
    XTX = XTX + r * np.eye(XTX.shape[0])
    
    XTX_inv = np.linalg.inv(XTX)
    w_full = XTX_inv.dot(X.T).dot(y)
    
    return w_full[0], w_full[1:]
```

Here, `r` is the regularization parameter α. You can adjust it to control the degree of regularization applied.

## Evaluating the Model with Regularization

Now, let's put our regularized linear regression model to the test. We'll train the model on our training data, apply it to validation data, and compute the RMSE:

```python
# Train
X_train = prepare_X(df_train)
w0, w = train_linear_regression_reg(X_train, y_train, r=0.01)

# Validation
X_val = prepare_X(df_val)
y_pred = w0 + X_val.dot(w)

rmse(y_val, y_pred)
```

Regularization not only helps avoid singular matrices but also often improves the model's performance. In this case, we observed a 0.5 improvement in RMSE compared to the non-regularized version.

## Conclusion

Regularization is a crucial technique in linear regression. It helps control the model's weights, preventing them from growing too large and overfitting the data. By adding a small number to the diagonal of the Gram matrix, we ensure that the inverse exists and stabilize our model. The regularization parameter α allows us to fine-tune the degree of regularization applied. In the next lesson, we'll delve deeper into how to choose the optimal α value.
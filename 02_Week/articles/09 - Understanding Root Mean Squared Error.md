# Understanding Root Mean Squared Error in Machine Learning

Machine learning is a fascinating field that encompasses a variety of models and techniques to make predictions and decisions based on data. One critical aspect of machine learning is model evaluation, which helps us understand how well a model is performing and whether it needs improvement. In this article, we will delve into one of the fundamental techniques for evaluating regression models, which is the Root Mean Squared Error (RMSE).

## Introduction

Before diving into RMSE, let's set the context. We are following a machine learning session, specifically **lesson nine** of **session two** of a **Machine Learning Zoom Camp**. In this lesson, the focus is on **evaluating regression models**.

## The Need for Model Evaluation

In the previous session, we trained our first model, which was a baseline model using only numerical features. We made predictions with this model and compared them to the actual values. We noticed that there was a difference between the predictions and the actual values, but we didn't have a way to quantify how bad the model's predictions were. This is precisely what we will address in this lesson using the Root Mean Squared Error.

## Understanding Root Mean Squared Error (RMSE)

Now, let's dive into the mathematical formulation of RMSE and break it down step by step.

RMSE stands for **Root Mean Squared Error**. It is a metric used to quantify the accuracy of a regression model's predictions by measuring the average squared difference between predicted and actual values. The formula for RMSE can be expressed as follows:

![RMSE Formula](https://latex.codecogs.com/gif.latex?%5Ctext%7BRMSE%7D%20%3D%20%5Csqrt%7B%5Cfrac%7B1%7D%7BM%7D%20%5Csum_%7Bi%3D1%7D%5E%7BM%7D%20%28%5Chat%7By%7D_i%20-%20y_i%29%5E2%7D)

Let's break down this formula into its constituent parts:

- **M** represents the number of observations in our dataset.
- **y** represents the actual values (the ground truth).
- **y_pred** represents the predictions made by our model.

The RMSE calculation involves these steps:

1. **Squared Difference**: Calculate the squared difference between each predicted value (**y_pred**) and the corresponding actual value (**y**).

2. **Mean Squared Error (MSE)**: Compute the average of these squared differences by summing them up and dividing by the number of observations (**M**).

3. **Root**: Finally, take the square root of the MSE to obtain the RMSE.

## An Example

Let's illustrate this with a simple example:

Suppose we have a set of predictions (**y_pred**) and actual values (**y**):

- **y_pred**: [10, 9, 11, 10.5]
- **y**: [9, 9, 10.5, 11.5]

Here's how we calculate RMSE step by step:

1. **Squared Difference**: Calculate the squared difference between each predicted and actual value:
   - (10 - 9)^2 = 1
   - (9 - 9)^2 = 0
   - (11 - 10.5)^2 = 0.25
   - (10.5 - 11.5)^2 = 1.00

2. **Mean Squared Error (MSE)**: Calculate the average of squared differences:
   - (1 + 0 + 0.25 + 1.00) / 4 = 0.875

3. **Root**: Take the square root of MSE:
   - RMSE = √0.875 ≈ 0.93

So, in this example, the RMSE is approximately 0.93, indicating that, on average, our model's predictions are off by about 0.93 units from the actual values.

## Implementing RMSE in Python

Now, let's see how we can implement RMSE in Python. Below is a Python function that calculates RMSE given the actual values (**y**) and the model's predictions (**y_pred**):

```python
import numpy as np

def rmse(y, y_pred):
    se = (y - y_pred) ** 2
    mse = se.mean()
    return np.sqrt(mse)
```

To use this function, you can simply call it with your actual values (**y**) and model predictions (**y_pred**):

```python
rmse(y_train, y_pred)
```

In the provided Jupyter Notebook code snippet, you can see this function in action. When applied to a specific dataset, it returns an RMSE value of approximately **0.7554**.

## Conclusion

Root Mean Squared Error (RMSE) is a valuable tool in machine learning for evaluating the accuracy of regression models. It provides a quantitative measure of how well a model's predictions match the actual values. By understanding RMSE and implementing it in your machine learning projects, you can gain insights into your model's performance and make informed decisions about model improvement. In the next lesson, as mentioned in the transcription, RMSE will be applied to the validation set to further evaluate the model.
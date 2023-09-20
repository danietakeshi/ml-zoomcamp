# Validating Machine Learning Models with Root Mean Squared Error (RMSE)

In our ongoing journey through the Machine Learning Zoom Camp, we've reached **lesson 10** of **session two**, and we're about to delve into the crucial topic of model validation. In previous lessons, we've constructed our very first baseline model, which relied on five numerical features. Additionally, we introduced a method for objectively assessing our model's quality: the Root Mean Square Error (RMSE).

However, there's a fundamental aspect of model evaluation that we need to address. In the past, we made a slight mistake in our validation process. Rather than accurately evaluating the model's performance, we applied it to the training dataset, effectively measuring its success on the data it already saw. What we should be doing instead is validation, and this is precisely what we'll focus on in this lesson.

## The Importance of Model Validation

Before we delve into the specifics of model validation, let's recall our past approach. We trained our linear regression model using the training dataset and subsequently calculated the RMSE on that very same training data. While this process had its merits, it didn't provide us with an accurate measure of how well our model would generalize to new, unseen data.

To rectify this, we need to adopt a more rigorous approach. Model validation should be conducted using a dedicated validation dataset, separate from the training dataset. This approach ensures that we evaluate the model's performance on data it hasn't encountered before, giving us a better understanding of how it will perform in real-world scenarios.

## Implementing Model Validation

To achieve model validation, we need to make some adjustments to our existing code. Let's break down the steps we'll take:

### 1. Prepare Feature Matrix

In our previous code, we created the feature matrix **X** directly from the training dataset. To make the process consistent across different datasets (training, validation, and test), we'll create a function called `prepare_X`. This function will accept a DataFrame as input and perform the following steps:

- Select the numerical columns.
- Fill in missing values (in our case, we fill missing values with zeros).
- Return the resulting numpy array.

Here's the `prepare_X` function:

```python
def prepare_X(df):
    df_num = df[base]
    df_num = df_num.fillna(0)
    return df_num.values
```

### 2. Training and Validation

Now that we have our `prepare_X` function, we can use it for both training and validation datasets. Here's how we update our code:

#### Training:
```python
# Prepare the feature matrix for training
X_train = prepare_X(df_train)

# Train the model
w0, w = train_linear_regression(X_train, y_train)
```

#### Validation:
```python
# Prepare the feature matrix for validation
X_val = prepare_X(df_val)

# Make predictions on the validation dataset
y_pred = w0 + X_val.dot(w)

# Calculate RMSE on the validation dataset
rmse(y_val, y_pred)
```

## Conclusion

With these updates, we've transformed our modeling process into a more robust and realistic one. We now have a dedicated validation dataset that allows us to assess the model's performance on unseen data accurately. By calculating the RMSE on this validation dataset, we gain insights into how well our model generalizes to real-world situations.

This marks a significant step in our journey through the Machine Learning Zoom Camp. Armed with accurate model validation, we can now focus on improving our model's performance based on real-world assessments. In future lessons, we will continue to refine our understanding of machine learning techniques and their practical applications. Stay tuned!
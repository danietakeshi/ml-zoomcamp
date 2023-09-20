# Tuning the Model's Regularization Parameter for Linear Regression

Welcome back to lesson 14 of Machine Learning Zoom Comp session 2! In this lesson, we will dive into the crucial task of finding the optimal regularization parameter for our linear regression model. As you might recall from the previous section, we discussed regularization as a means to address the issue of duplicated columns in our data. We also observed that the choice of the regularization parameter, often denoted as "𝑅," significantly influences the quality of our model. Our goal now is to determine the best value for this regularization parameter, and we'll accomplish this using a validation set.

## The Quest for the Best 𝑅

To embark on our quest to find the best 𝑅, we'll take a systematic approach. We'll start by experimenting with various values of 𝑅, beginning from zero and gradually increasing it. This process allows us to explore the entire spectrum of regularization strengths. Here's the list of 𝑅 values we'll explore:

```python
[0.0, 0.0000001, 0.000001, 0.00001, 0.0001, 0.0001, 0.001, 0.1, 1, 10]
```

Let's break down what we'll do for each 𝑅 value in this list:

1. **Training:** We'll prepare our training dataset, which involves any necessary data preprocessing. Then, we'll train our linear regression model using the given 𝑅 value.

2. **Validation:** After training, we'll apply our trained model to the validation set and predict the target variable. This step allows us to evaluate the model's performance on unseen data.

3. **Scoring:** We'll calculate the Root Mean Square Error (RMSE) between the actual target values and the predictions made by our model. This score quantifies how well our model is performing, with lower values indicating better performance.

4. **Logging:** Finally, we'll log the regularization parameter 𝑅, the bias term (𝑤0), and the RMSE score.

## Exploring 𝑅 Values

Let's go ahead and explore the impact of different 𝑅 values on our model. We'll iterate through our 𝑅 list and print the results:

```python
for r in [0.0, 0.0000001, 0.000001, 0.00001, 0.0001, 0.0001, 0.001, 0.1, 1, 10]:
    # Train
    X_train = prepare_X(df_train)
    w0, w = train_linear_regression_reg(X_train, y_train, r=r)

    # Validation
    X_val = prepare_X(df_val)
    y_pred = w0 + X_val.dot(w)

    score = rmse(y_val, y_pred)
    
    print(r, w0, score)
```

When we run this code, we obtain a table of results with 𝑅, bias term (𝑤0), and RMSE scores for each 𝑅 value. This table provides insights into how different levels of regularization affect our model's performance.

## Analyzing the Results

As we examine the results, we notice several interesting observations:

- For 𝑅 = 0.0 (no regularization), the bias term (𝑤0) is substantial, and the RMSE is quite high.
- As we introduce even a small amount of regularization (e.g., 𝑅 = 0.0000001), both the bias term and RMSE improve significantly.
- The RMSE remains relatively stable for a range of 𝑅 values but starts to degrade as 𝑅 becomes too large (e.g., 𝑅 = 10).
- Smaller 𝑅 values result in larger bias terms, but this effect diminishes as regularization strength increases.

Upon closer inspection, we identify a promising candidate for 𝑅: 𝑅 = 0.01. At this point, the model's performance on the validation set remains strong, the bias term is not excessively large, and the RMSE is favorable.

## Training the Final Model

With our chosen regularization parameter 𝑅 = 0.01, we can now train our final linear regression model:

```python
r = 0.01
# Train
X_train = prepare_X(df_train)
w0, w = train_linear_regression_reg(X_train, y_train, r=r)

# Validation
X_val = prepare_X(df_val)
y_pred = w0 + X_val.dot(w)

score = rmse(y_val, y_pred)

print(r, w0, score)
```

This code trains the model using the selected regularization parameter and prints out the final RMSE score on the validation set.

## Conclusion and Next Steps

In this lesson, we've successfully tuned our linear regression model by identifying the optimal regularization parameter 𝑅. Our chosen value, 𝑅 = 0.01, strikes a balance between model performance and regularization strength.

In the next lecture, we will take this well-tuned model and put it to the ultimate test: evaluating its performance on the test dataset. Stay tuned for the exciting results in the upcoming lesson!
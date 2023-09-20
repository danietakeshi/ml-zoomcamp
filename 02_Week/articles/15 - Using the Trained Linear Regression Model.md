# Using the Trained Linear Regression Model for Car Price Prediction

Welcome back to Lesson 15 of Machine Learning ZoomCup Session 2! In the previous lesson, we successfully found the best parameter for our linear regression model. Now, in this lesson, we're going to take our well-tuned model and put it to practical use. Specifically, we will train the final model and use it to make real-world predictions.

## Training the Final Model

Before we dive into predictions, let's clarify what we mean by training the final model. So far, we've been working with a dataset split into three parts: training, validation, and test datasets. We've trained our model on the training dataset, validated it using the validation dataset, and fine-tuned it to achieve the best performance. Now, instead of training solely on the training dataset, we'll combine the training and validation datasets into one and train our final model on this "full train" dataset. This approach allows us to make the most of our available data.

Let's go ahead and combine the training and validation datasets:

```python
df_full_train = pd.concat([df_train, df_val])
df_full_train = df_full_train.reset_index(drop=True)
```

Now, we have a single dataset, `df_full_train`, that contains both the training and validation data. This combined dataset will be used to train our final model.

## Preparing the Feature Matrix

Next, we need to prepare the feature matrix for this combined dataset, just like we did before:

```python
X_full_train = prepare_X(df_full_train)
```

## Combining the Target Values

To train our final model, we also need to combine the target values for the training and validation datasets. We can use NumPy's `concatenate` function for this purpose:

```python
y_full_train = np.concatenate([y_train, y_val])
```

Now that we have the feature matrix (`X_full_train`) and the target values (`y_full_train`), we are ready to train the final model. We'll use the same regularization parameter (`r=0.001`) that we determined to be the best earlier:

```python
w0, w = train_linear_regression_reg(X_full_train, y_full_train, r=0.001)
```

The `w0` and `w` values represent the bias term and the model weights, respectively, for our final linear regression model.

## Predicting Car Prices

With the final model in hand, we can use it to predict the price of a car. To do this, we'll simulate a scenario where a user provides us with information about a car, and we use our model to estimate the car's price. Here's how it works:

1. We create a dictionary that contains all the relevant information about the car. This could be information collected from a website or app where users input details about their cars.

2. We convert this dictionary into a DataFrame with a single row, which simulates a scenario where a user's input is converted into a structured format for prediction.

3. We prepare the feature matrix for this single-row DataFrame using our `prepare_X` function.

4. We use our final model to predict the car's price by applying the model to the feature matrix.

5. Since our model outputs the logarithm of the price, we need to exponentiate it to get the actual price.

Let's see this process in action. We'll use a sample car entry from our test dataset:

```python
car = df_test.iloc[20].to_dict()
df_small = pd.DataFrame([car])
X_small = prepare_X(df_small)
y_pred = w0 + X_small.dot(w)
predicted_price = np.expm1(y_pred[0])
```

In this example, we've taken a car entry from our test dataset and treated it as a new, unseen car. After processing the data through our model, we obtain an estimated car price. For this specific car, our model predicts a price of approximately $39,611.

## Model Evaluation

It's worth noting that we compared our prediction to the actual price in the test dataset to assess the model's accuracy. In this case, the actual price for the car in question was approximately $35,000, so our prediction was reasonably close.

## Conclusion

In this lesson, we have successfully trained our final linear regression model and used it to make predictions on car prices. We demonstrated how to convert user-provided information into structured data, feed it into the model, and obtain a price estimate.

This marks the end of our journey in this machine learning session. We hope you've gained valuable insights into the world of machine learning and data analysis. Remember that the skills you've acquired here can be applied to a wide range of real-world problems, from predicting car prices to tackling more complex challenges. Keep exploring and applying your knowledge in exciting new ways!
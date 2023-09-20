# Setting Up the Validation Framework: Splitting Data into Train, Validation, and Test Sets

In this article, we will discuss how to set up a validation framework in Python using a Jupyter Notebook. We'll be working with a dataset and dividing it into three parts: a training set, a validation set, and a test set. This process is crucial for model development and evaluation.

## Introduction

In machine learning, it's essential to validate the performance of a model on data that it hasn't seen during training. To achieve this, we divide our dataset into three distinct subsets: the training set, the validation set, and the test set.

- The **training set** is used to train the machine learning model.
- The **validation set** is used to fine-tune the model and evaluate its performance during the training process.
- The **test set** is used to assess the model's final performance after training.

In this tutorial, we'll use Python, specifically Pandas and NumPy, to split our dataset into these three sets.

## Code Implementation

Let's start by breaking down the code step by step:

```python
n = len(df.index)

n_val = int(n * 0.2)
n_test = int(n * 0.2)
n_train = n - n_val - n_test
```

Here, we calculate the sizes of the validation, test, and training sets. We assume that the validation and test sets should each contain 20% of the total data, leaving the remaining 60% for the training set. The variables `n_val`, `n_test`, and `n_train` represent the sizes of these respective sets.

```python
n, n_val, n_test,  n_train
```

We check the calculated sizes to ensure they match our expectations. In this example, the total number of records in the dataset (`n`) is 11,914. Thus, we have 2,382 records in both the validation and test sets, and 7,150 records in the training set.

Next, we inspect the first 10 records in our dataset using `df.iloc[:10]`. This helps us understand the structure of the data and the order of records.

Now that we have determined the sizes of the subsets and inspected the data, we can proceed with splitting the data.

## Data Splitting

We will split our dataset into three subsets: `train`, `validation`, and `test`. To ensure randomness and avoid any potential bias, we will shuffle the data before splitting.

```python
import numpy as np

# Create an index array from 0 to (n-1)
idx = np.arange(n)

# Shuffle the index array
np.random.seed(2)  # Set a random seed for reproducibility
np.random.shuffle(idx)

# Split the index array into train, validation, and test sets
train_idx = idx[:n_train]
val_idx = idx[n_train:n_train + n_val]
test_idx = idx[n_train + n_val:]

# Create the train, validation, and test dataframes
df_train = df.iloc[train_idx].reset_index(drop=True)
df_val = df.iloc[val_idx].reset_index(drop=True)
df_test = df.iloc[test_idx].reset_index(drop=True)
```

Here's a breakdown of the code:

- We import the NumPy library, which is useful for generating random numbers and shuffling data.

- We create an index array `idx` from 0 to `(n-1)`, where `n` is the total number of records in our dataset.

- We set a random seed using `np.random.seed(2)` to ensure reproducibility. The seed value can be any integer.

- We shuffle the `idx` array to randomize the order of records. This step is crucial to remove any inherent order or bias in the dataset.

- We split the shuffled index array into three parts: `train_idx`, `val_idx`, and `test_idx`. These indices represent the records assigned to each subset.

- Finally, we create three dataframes, `df_train`, `df_val`, and `df_test`, by selecting rows from the original dataframe `df` based on the respective index arrays. We also reset the index for each dataframe to start from 0.

## Preparing the Target Variable (Y)

Before we finish, we need to make sure our target variable, which in this case is the 'MSRP' (Manufacturer's Suggested Retail Price), is appropriately transformed. It's common in machine learning to apply transformations to target variables to make their distributions more suitable for modeling. In this example, we'll use the natural logarithm transformation.

```python
# Apply the natural logarithm transformation to the 'MSRP' column
df_train['MSRP'] = np.log1p(df_train['MSRP'])
df_val['MSRP'] = np.log1p(df_val['MSRP'])
df_test['MSRP'] = np.log1p(df_test['MSRP'])

# Create target variable arrays
y_train = df_train['MSRP'].values
y_val = df_val['MSRP'].values
y_test = df_test['MSRP'].values



# Drop the 'MSRP' column from the feature sets
X_train = df_train.drop(columns=['MSRP']).values
X_val = df_val.drop(columns=['MSRP']).values
X_test = df_test.drop(columns=['MSRP']).values
```

Here, we perform the following actions:

- Apply the natural logarithm transformation (`np.log1p()`) to the 'MSRP' column of each dataframe. This transformation helps stabilize the variance in the target variable and make it more suitable for regression tasks.

- Create arrays `y_train`, `y_val`, and `y_test` containing the transformed target variable.

- Create feature sets `X_train`, `X_val`, and `X_test` by dropping the 'MSRP' column from the respective dataframes and converting the remaining data to NumPy arrays.

## Conclusion

In this tutorial, we've set up a validation framework in Python for splitting data into training, validation, and test sets. This is a crucial step in machine learning model development and evaluation. Additionally, we've demonstrated how to prepare the target variable using a natural logarithm transformation, which can help improve the performance of regression models.

You can now use these subsets for model training, hyperparameter tuning, and evaluating your machine learning models. Remember that the random seed used for shuffling ensures reproducibility, which is essential for consistent results in your data analysis and modeling efforts.
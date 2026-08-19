# MICE — Multivariate Imputation by Chained Equations

A short and simple guide to **MICE (Multivariate Imputation by Chained Equations)** for handling missing values in a dataset.

## What is MICE?

MICE is a multivariate imputation technique used to fill missing values by using the relationships between different columns in the dataset.

It is also commonly called **Multiple Imputation by Chained Equations**.

## Types of Missing Data

* **MCAR — Missing Completely At Random:** Missingness is unrelated to the data.
* **MAR — Missing At Random:** Missingness can be explained using other available variables.
* **MNAR — Missing Not At Random:** Missingness depends on the missing value itself or an unobserved factor.

MICE generally works best when the data is **MAR**.

## How MICE Works

The basic process is:

1. Replace missing values with the **mean** of their respective columns.
2. Start from the first column containing missing values.
3. Temporarily treat its missing values as missing again.
4. Use the other columns as input features.
5. Train a machine learning model, such as:

   * Linear Regression
   * Random Forest
   * Decision Tree
6. Predict the missing values.
7. Move to the next column and repeat the process.
8. Continue through all columns containing missing values.
9. Repeat the complete process for multiple iterations.
10. Stop when the imputed values become stable or the difference between iterations becomes sufficiently small.

## Simple Example

Suppose our dataset contains:

| R&D Spend | Administration | Marketing | Profit |
| --------- | -------------- | --------- | ------ |
| 165349    | 136898         | 471784    | 192262 |
| 162598    | NaN            | 443899    | 191792 |
| NaN       | 151377         | 407935    | 182902 |

First, missing values are temporarily filled using column means.

Then MICE uses the available columns to predict better values for the missing entries.

The process is repeated until the values converge.

## Why Use MICE?

### Advantages

* Uses relationships between multiple variables.
* Usually gives better estimates than simple mean/median imputation.
* Can use different machine learning models.
* Useful for multivariate datasets.

### Disadvantages

* Computationally slower than simple imputation.
* Can require more memory.
* Multiple iterations may be expensive for large datasets.
* Results depend on the model used for prediction.

## Important Concept

MICE is an **iterative process**:

```text
Initial Mean Imputation
        ↓
Column 1 Prediction
        ↓
Column 2 Prediction
        ↓
Column 3 Prediction
        ↓
Iteration 1 Complete
        ↓
Repeat
        ↓
Iteration 2
        ↓
Repeat until convergence
```





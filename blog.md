---
title: "Blog"
---

# Cleaning and Analyzing Data with Pandas

## Introduction

In many data science projects, the hardest part is not modeling. It is
cleaning the data.

Real datasets often have: 
- Missing values 
- Inconsistent column names 
- Wrong data types
- Duplicate rows

If we do not clean the data correctly, our analysis can be misleading.

In this tutorial, I will show a simple workflow for cleaning and
analyzing a dataset using **pandas**.

We will: 
1. Load a dataset
2. Inspect it
3. Clean missing values
4. Fix column names
5. Remove duplicates
6. Do a small analysis

------------------------------------------------------------------------

## 1) Setup: Import and Load Data

``` python
import pandas as pd

df = pd.read_csv("titanic.csv")
```

If you do not have this dataset, you can download it from Kaggle or use
any CSV file you already have.

------------------------------------------------------------------------

## 2) Inspect the Dataset

``` python
df.head()
```

``` python
df.info()
```

``` python
df.describe()
```

These help you understand: 
- `head()` shows the first rows
- `info()` shows column types and missing values
- `describe()` shows summary statistics

------------------------------------------------------------------------

## 3) Check for Missing Values

``` python
df.isnull().sum()
```

Example: fill missing age values with the median.

``` python
df["Age"] = df["Age"].fillna(df["Age"].median())
```

------------------------------------------------------------------------

## 4) Clean Column Names

``` python
df.columns = df.columns.str.lower().str.replace(" ", "_")
```

------------------------------------------------------------------------

## 5) Remove Duplicate Rows

``` python
df = df.drop_duplicates()
```

------------------------------------------------------------------------

## 6) Simple Analysis Example

``` python
survival_rate = df["survived"].mean()
survival_rate
```

Because `survived` is coded as 0 and 1, the mean gives:

$$
\text{Survival Rate} = \frac{\text{Number of Survivors}}{\text{Total Passengers}}
$$

------------------------------------------------------------------------

## 7) Grouped Analysis Example

``` python
df.groupby("sex")["survived"].mean()
```

------------------------------------------------------------------------

## 8) Summary Table of the Workflow

| Step                | Why it matters          | Example tool                |
|---------------------|------------------------|-----------------------------|
| Inspect data        | Understand structure   | `head()`, `info()`          |
| Missing values      | Avoid biased results   | `isnull().sum()`            |
| Fill missing        | Improve data quality   | `fillna()`                  |
| Clean column names  | Easier coding          | `str.lower()`, `replace()`  |
| Remove duplicates   | Prevent distortion     | `drop_duplicates()`         |
| Basic analysis      | Get insights           | `mean()`, `groupby()`       |


------------------------------------------------------------------------

## Conclusion

Cleaning data is one of the most important skills in data science.

Following a clear structure helps you: 
- Stay organized
- Avoid mistakes
- Produce better analysis

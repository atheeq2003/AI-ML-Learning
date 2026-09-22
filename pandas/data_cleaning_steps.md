# Data Cleaning using Pandas

## 📌 Project Overview

This project focuses on cleaning and preparing a raw dataset using **Python and Pandas** before performing Exploratory Data Analysis (EDA).

The cleaning process handles missing values, duplicate records, incorrect data types, inconsistent text values, unwanted columns, and outliers.

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Jupyter Notebook / Google Colab

---

# 📋 Data Cleaning Steps

## 1. Import Required Libraries

```python
import pandas as pd
import numpy as np
```

## 2. Load the Dataset

```python
df = pd.read_csv("data.csv")
```

Check the first few records:

```python
print(df.head())
```

---

## 3. Understand the Dataset

Check the number of rows and columns:

```python
print(df.shape)
```

Check column names:

```python
print(df.columns)
```

Check data types and missing values:

```python
print(df.info())
```

Generate basic statistics:

```python
print(df.describe())
```

---

## 4. Check Missing Values

```python
print(df.isnull().sum())
```

Calculate the percentage of missing values:

```python
missing_percentage = (df.isnull().sum() / len(df)) * 100
print(missing_percentage)
```

---

## 5. Handle Missing Values

### Numerical columns

Fill missing values with the median:

```python
df["age"] = df["age"].fillna(df["age"].median())
```

### Categorical columns

Fill missing values with the mode:

```python
df["gender"] = df["gender"].fillna(df["gender"].mode()[0])
```

### Remove rows with missing values

```python
df = df.dropna()
```

Use this only when removing those records is appropriate.

---

## 6. Check and Remove Duplicate Records

Check duplicates:

```python
print(df.duplicated().sum())
```

Remove duplicates:

```python
df = df.drop_duplicates()
```

---

## 7. Clean Column Names

```python
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(" ", "_")
)
```

Example:

```text
Customer Name → customer_name
Annual Salary → annual_salary
```

---

## 8. Remove Unnecessary Columns

```python
df = df.drop(columns=["unnamed:_0"], errors="ignore")
```

Or:

```python
df = df.drop(columns=["unnecessary_column"])
```

---

## 9. Correct Data Types

Convert numerical columns:

```python
df["age"] = pd.to_numeric(df["age"], errors="coerce")
```

Convert dates:

```python
df["date"] = pd.to_datetime(df["date"], errors="coerce")
```

Check the result:

```python
print(df.dtypes)
```

---

## 10. Clean Text Data

Remove unnecessary spaces:

```python
df["city"] = df["city"].str.strip()
```

Standardize capitalization:

```python
df["city"] = df["city"].str.title()
```

Convert text to lowercase:

```python
df["email"] = df["email"].str.lower()
```

---

## 11. Handle Inconsistent Values

Example:

```python
df["gender"] = df["gender"].replace({
    "M": "Male",
    "m": "Male",
    "F": "Female",
    "f": "Female"
})
```

This makes different representations consistent.

---

## 12. Identify Invalid Values

For example, age should not be negative:

```python
df.loc[df["age"] < 0, "age"] = np.nan
```

Then handle the missing value:

```python
df["age"] = df["age"].fillna(df["age"].median())
```

---

## 13. Detect Outliers

Using the IQR method:

```python
Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)

IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[
    (df["salary"] < lower_bound) |
    (df["salary"] > upper_bound)
]

print(outliers)
```

Remove outliers if appropriate:

```python
df = df[
    (df["salary"] >= lower_bound) &
    (df["salary"] <= upper_bound)
]
```

---

## 14. Reset the Index

After removing rows:

```python
df = df.reset_index(drop=True)
```

---

## 15. Verify the Cleaned Dataset

Check missing values:

```python
print(df.isnull().sum())
```

Check duplicates:

```python
print(df.duplicated().sum())
```

Check data types:

```python
print(df.dtypes)
```

Check dataset size:

```python
print(df.shape)
```

Check statistics:

```python
print(df.describe())
```

---

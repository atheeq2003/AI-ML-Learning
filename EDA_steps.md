
# 📊 Exploratory Data Analysis (EDA) — AI/ML

A reusable **Exploratory Data Analysis (EDA)** template for AI/ML projects using  **Python, NumPy, Pandas, Matplotlib, and Seaborn** .

The goal of EDA is to understand the dataset, identify patterns, detect problems, visualize relationships, and prepare clean data for Machine Learning.

---

# 📌 Table of Contents

1. [What is EDA?](https://chatgpt.com/?temporary-chat=true#-what-is-eda)
2. [EDA Workflow](https://chatgpt.com/?temporary-chat=true#-eda-workflow)
3. [1. Import Libraries](https://chatgpt.com/?temporary-chat=true#1-import-libraries)
4. [2. Load Dataset](https://chatgpt.com/?temporary-chat=true#2-load-dataset)
5. [3. Understand the Dataset](https://chatgpt.com/?temporary-chat=true#3-understand-the-dataset)
6. [4. Data Types](https://chatgpt.com/?temporary-chat=true#4-data-types)
7. [5. Statistical Summary](https://chatgpt.com/?temporary-chat=true#5-statistical-summary)
8. [6. Missing Values](https://chatgpt.com/?temporary-chat=true#6-missing-values)
9. [7. Duplicate Values](https://chatgpt.com/?temporary-chat=true#7-duplicate-values)
10. [8. Unique Values](https://chatgpt.com/?temporary-chat=true#8-unique-values)
11. [9. Numerical Columns](https://chatgpt.com/?temporary-chat=true#9-numerical-columns)
12. [10. Categorical Columns](https://chatgpt.com/?temporary-chat=true#10-categorical-columns)
13. [11. Outlier Detection](https://chatgpt.com/?temporary-chat=true#11-outlier-detection)
14. [12. Data Visualization](https://chatgpt.com/?temporary-chat=true#12-data-visualization)
15. [13. Correlation Analysis](https://chatgpt.com/?temporary-chat=true#13-correlation-analysis)
16. [14. GroupBy Analysis](https://chatgpt.com/?temporary-chat=true#14-groupby-analysis)
17. [15. Feature Relationships](https://chatgpt.com/?temporary-chat=true#15-feature-relationships)
18. [16. Data Cleaning](https://chatgpt.com/?temporary-chat=true#16-data-cleaning)
19. [17. Feature Engineering](https://chatgpt.com/?temporary-chat=true#17-feature-engineering)
20. [18. ML Preparation](https://chatgpt.com/?temporary-chat=true#18-ml-preparation)
21. [19. Final Insights](https://chatgpt.com/?temporary-chat=true#19-final-insights)

---

# 🔎 What is EDA?

**Exploratory Data Analysis (EDA)** is the process of analyzing a dataset before building a Machine Learning model.

EDA helps us answer questions such as:

* What does the dataset contain?
* How many rows and columns are there?
* Which columns are numerical?
* Which columns are categorical?
* Are there missing values?
* Are there duplicate records?
* Are there outliers?
* What are the most important features?
* Which variables are related?
* Are there patterns or trends?
* Is the dataset suitable for Machine Learning?

### Basic EDA Flow

```text
Raw Dataset
     ↓
Load Dataset
     ↓
Understand Data
     ↓
Clean Data
     ↓
Handle Missing Values
     ↓
Handle Duplicates
     ↓
Detect Outliers
     ↓
Analyze Statistics
     ↓
Visualize Data
     ↓
Correlation Analysis
     ↓
Feature Engineering
     ↓
ML-Ready Dataset
```

---

# 🛠️ Libraries Used

| Library    | Purpose                        |
| ---------- | ------------------------------ |
| NumPy      | Numerical operations           |
| Pandas     | Data manipulation and analysis |
| Matplotlib | Data visualization             |
| Seaborn    | Statistical visualization      |

Install them:

```bash
pip install numpy pandas matplotlib seaborn
```

---

# 1. Import Libraries

```python
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
import seaborn as sns
```

Optional settings:

```python
pd.set_option("display.max_columns", None)
pd.set_option("display.max_rows", 100)

sns.set_theme()
```

---

# 2. Load Dataset

## CSV

```python
df = pd.read_csv("dataset.csv")
```

## Excel

```python
df = pd.read_excel("dataset.xlsx")
```

## JSON

```python
df = pd.read_json("dataset.json")
```

---

# 3. Understand the Dataset

## Display first rows

```python
df.head()
```

Display first 10 rows:

```python
df.head(10)
```

## Display last rows

```python
df.tail()
```

## Random samples

```python
df.sample(5)
```

---

## Dataset Shape

```python
df.shape
```

Output:

```text
(rows, columns)
```

Example:

```text
(10000, 15)
```

This means:

* 10,000 rows
* 15 columns

---

## Column Names

```python
df.columns
```

Convert to list:

```python
df.columns.tolist()
```

---

## Basic Information

```python
df.info()
```

This tells us:

* Number of rows
* Column names
* Data types
* Non-null values
* Memory usage

---

# 4. Data Types

Check data types:

```python
df.dtypes
```

### Common Data Types

| Type           | Meaning               |
| -------------- | --------------------- |
| `int64`      | Integer               |
| `float64`    | Decimal               |
| `object`     | Usually text/category |
| `bool`       | True/False            |
| `datetime64` | Date/time             |

---

## Select Numerical Columns

```python
df.select_dtypes(include=np.number)
```

## Select Categorical Columns

```python
df.select_dtypes(include="object")
```

---

# 5. Statistical Summary

For numerical columns:

```python
df.describe()
```

Important statistics:

| Statistic | Meaning                   |
| --------- | ------------------------- |
| count     | Number of non-null values |
| mean      | Average                   |
| std       | Standard deviation        |
| min       | Minimum                   |
| 25%       | First quartile            |
| 50%       | Median                    |
| 75%       | Third quartile            |
| max       | Maximum                   |

---

## Include Categorical Data

```python
df.describe(include="all")
```

---

# 6. Missing Values

Missing values are one of the first things we should check.

## Count Missing Values

```python
df.isnull().sum()
```

## Missing Percentage

```python
missing_percentage = df.isnull().mean() * 100

print(missing_percentage)
```

---

## Visualize Missing Values

```python
plt.figure(figsize=(10, 6))

sns.heatmap(df.isnull(), cbar=False)

plt.title("Missing Values")
plt.show()
```

---

## Remove Missing Rows

Use carefully:

```python
df.dropna()
```

---

## Fill Missing Values

### Mean

```python
df["column"].fillna(df["column"].mean(), inplace=True)
```

### Median

```python
df["column"].fillna(df["column"].median(), inplace=True)
```

### Mode

```python
df["column"].fillna(df["column"].mode()[0], inplace=True)
```

### General Rule

```text
Numerical → Mean / Median

Categorical → Mode

Time Series → Forward Fill / Backward Fill
```

---

# 7. Duplicate Values

Check duplicates:

```python
df.duplicated().sum()
```

Display duplicates:

```python
df[df.duplicated()]
```

Remove duplicates:

```python
df = df.drop_duplicates()
```

Check the new shape:

```python
df.shape
```

---

# 8. Unique Values

## Number of Unique Values

```python
df["column"].nunique()
```

## Display Unique Values

```python
df["column"].unique()
```

## Frequency of Values

```python
df["column"].value_counts()
```

---

## Example

For a gender column:

```python
df["Gender"].value_counts()
```

Possible output:

```text
Male      5200
Female    4700
Other      100
```

---

# 9. Numerical Columns

Identify numerical columns:

```python
numeric_columns = df.select_dtypes(include=np.number).columns

print(numeric_columns)
```

---

## Mean

```python
df["column"].mean()
```

## Median

```python
df["column"].median()
```

## Minimum

```python
df["column"].min()
```

## Maximum

```python
df["column"].max()
```

## Standard Deviation

```python
df["column"].std()
```

---

# 📊 Numerical Data Visualization

## Histogram

Used to understand the distribution of a variable.

```python
plt.figure(figsize=(8, 5))

sns.histplot(df["column"], kde=True)

plt.title("Distribution of Column")
plt.xlabel("Column")
plt.ylabel("Frequency")

plt.show()
```

### Questions to ask:

* Is the data normally distributed?
* Is it skewed?
* Are there multiple peaks?
* Are there unusual values?

---

## Box Plot

Useful for detecting outliers.

```python
plt.figure(figsize=(8, 5))

sns.boxplot(x=df["column"])

plt.title("Box Plot")
plt.show()
```

---

# 10. Categorical Columns

Find categorical columns:

```python
categorical_columns = df.select_dtypes(include="object").columns

print(categorical_columns)
```

---

## Frequency Distribution

```python
df["category"].value_counts()
```

---

## Bar Plot

```python
plt.figure(figsize=(8, 5))

sns.countplot(data=df, x="category")

plt.title("Category Distribution")
plt.xticks(rotation=45)

plt.show()
```

---

# 11. Outlier Detection

Outliers are observations that are unusually far from the rest of the data.

## IQR Method

Calculate Q1:

```python
Q1 = df["column"].quantile(0.25)
```

Calculate Q3:

```python
Q3 = df["column"].quantile(0.75)
```

Calculate IQR:

```python
IQR = Q3 - Q1
```

Lower Bound:

```python
lower_bound = Q1 - 1.5 * IQR
```

Upper Bound:

```python
upper_bound = Q3 + 1.5 * IQR
```

Find outliers:

```python
outliers = df[
    (df["column"] < lower_bound) |
    (df["column"] > upper_bound)
]

print(outliers)
```

Number of outliers:

```python
len(outliers)
```

---

# 12. Data Visualization

Visualization is one of the most important parts of EDA.

---

## 📊 Histogram

```python
sns.histplot(df["column"], kde=True)

plt.show()
```

**Purpose:** Understand distribution.

---

## 📦 Box Plot

```python
sns.boxplot(x=df["column"])

plt.show()
```

**Purpose:** Detect outliers.

---

## 📊 Count Plot

```python
sns.countplot(data=df, x="category")

plt.show()
```

**Purpose:** Analyze categorical distributions.

---

## 🔵 Scatter Plot

Used to understand relationships between two numerical variables.

```python
sns.scatterplot(
    data=df,
    x="feature1",
    y="feature2"
)

plt.show()
```

---

## 📈 Line Plot

Useful for time-series data.

```python
sns.lineplot(
    data=df,
    x="date",
    y="value"
)

plt.xticks(rotation=45)

plt.show()
```

---

## 🥧 Pie Chart

```python
df["category"].value_counts().plot(
    kind="pie",
    autopct="%1.1f%%"
)

plt.ylabel("")
plt.show()
```

Use pie charts only when the number of categories is small.

---

# 13. Correlation Analysis

Correlation tells us how strongly numerical variables are related.

```python
correlation = df.corr(numeric_only=True)

print(correlation)
```

---

## Correlation Heatmap

```python
plt.figure(figsize=(12, 8))

sns.heatmap(
    correlation,
    annot=True,
    cmap="coolwarm"
)

plt.title("Correlation Heatmap")
plt.show()
```

### Correlation Range

```text
-1 ←──────── 0 ────────→ +1
Strong        No         Strong
Negative    Correlation  Positive
```

Examples:

```text
+0.90 → Strong positive relationship

+0.10 → Very weak positive relationship

 0.00 → Little/no linear relationship

-0.80 → Strong negative relationship
```

⚠️ **Important:** Correlation does not automatically mean causation.

---

# 14. GroupBy Analysis

`groupby()` is extremely useful for EDA.

## Average

```python
df.groupby("category")["sales"].mean()
```

## Sum

```python
df.groupby("category")["sales"].sum()
```

## Count

```python
df.groupby("category")["sales"].count()
```

## Multiple Aggregations

```python
df.groupby("category")["sales"].agg(
    ["mean", "median", "min", "max", "sum"]
)
```

---

# 15. Feature Relationships

Compare two or more features.

## Numerical vs Numerical

Use:

```text
Scatter Plot
Correlation
```

Example:

```python
sns.scatterplot(
    data=df,
    x="age",
    y="income"
)

plt.show()
```

---

## Categorical vs Numerical

Use:

```text
Box Plot
Violin Plot
Bar Plot
```

Example:

```python
sns.boxplot(
    data=df,
    x="category",
    y="income"
)

plt.xticks(rotation=45)

plt.show()
```

---

## Categorical vs Categorical

Use:

```python
pd.crosstab(
    df["category1"],
    df["category2"]
)
```

Visualization:

```python
sns.heatmap(
    pd.crosstab(df["category1"], df["category2"]),
    annot=True,
    fmt="d"
)

plt.show()
```

---

# 16. Data Cleaning

After understanding the dataset, clean it.

### Typical Cleaning Tasks

```text
Missing Values
      ↓
Duplicate Values
      ↓
Incorrect Data Types
      ↓
Invalid Values
      ↓
Outliers
      ↓
Inconsistent Categories
      ↓
Clean Dataset
```

---

## Rename Columns

```python
df.rename(
    columns={
        "old_name": "new_name"
    },
    inplace=True
)
```

---

## Convert Data Type

```python
df["age"] = df["age"].astype(int)
```

---

## Convert to Date

```python
df["date"] = pd.to_datetime(df["date"])
```

---

## Remove Unnecessary Columns

```python
df.drop(
    columns=["unnecessary_column"],
    inplace=True
)
```

---

## Clean Text

```python
df["name"] = df["name"].str.strip()
```

Convert to lowercase:

```python
df["name"] = df["name"].str.lower()
```

---

# 17. Feature Engineering

Feature engineering means creating useful new features from existing data.

---

## Example: Age Group

```python
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 18, 35, 60, 100],
    labels=[
        "Child",
        "Young Adult",
        "Adult",
        "Senior"
    ]
)
```

---

## Extract Date Features

```python
df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day
df["day_of_week"] = df["date"].dt.day_name()
```

---

## Example: Total Amount

```python
df["total_amount"] = (
    df["quantity"] * df["price"]
)
```

---

# 18. ML Preparation

After EDA and cleaning, prepare the dataset for Machine Learning.

---

## Separate Features and Target

```python
X = df.drop("target", axis=1)

y = df["target"]
```

Where:

```text
X → Input Features

y → Target / Output
```

---

## Categorical Encoding

Example:

```python
df = pd.get_dummies(
    df,
    columns=["category"],
    drop_first=True
)
```

---

## Train-Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Typical split:

```text
80% → Training
20% → Testing
```

---

# 19. Final EDA Insights

At the end of the EDA, write the important findings.

## Dataset Overview

```text
Dataset Name:
Number of Rows:
Number of Columns:
Time Period:
Data Source:
```

## Data Quality

```text
Missing Values:
Duplicate Values:
Outliers:
Incorrect Data Types:
```

## Important Findings

```text
1. ______________________________

2. ______________________________

3. ______________________________

4. ______________________________

5. ______________________________
```

## Important Relationships

```text
Feature 1 ↔ Feature 2:
Relationship:

Feature 3 ↔ Feature 4:
Relationship:
```

## ML Considerations

```text
Important Features:
Potential Target:
Features requiring encoding:
Features requiring scaling:
Potential outliers:
Potential data leakage:
```

---

# 🧠 EDA Questions to Ask

While performing EDA, don't just run commands. Ask questions.

### Dataset

* What is the size of the dataset?
* What does each row represent?
* What does each column represent?
* What is the time period covered?
* Where did the data come from?

### Data Quality

* Are there missing values?
* Are there duplicates?
* Are there invalid values?
* Are data types correct?
* Are categories consistent?

### Numerical Data

* What is the average?
* What is the median?
* What is the range?
* Is the distribution skewed?
* Are there outliers?

### Categorical Data

* Which category occurs most often?
* Which category occurs least often?
* Is the dataset imbalanced?

### Relationships

* Which features are correlated?
* Are there strong relationships?
* Are there unexpected patterns?
* Are there possible redundant features?

### ML Preparation

* What is the target variable?
* Which features are useful?
* Which features should be removed?
* Which features require encoding?
* Which features require scaling?
* Is there possible data leakage?

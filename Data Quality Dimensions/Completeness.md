# Measuring Data Completeness in a Dataset

**Completeness** is a key quality indicator in data analysis. It refers to how much of your data is present versus missing. Missing or incomplete data can impact decision-making, reporting, and model accuracy.

One common way to measure completeness is by checking the percentage of non-missing values in each column of your dataset.


**Example: Evaluating Completeness with Pandas**

```python
import pandas as pd

# Create a dataset with missing entries

data = {
    'EmployeeID': [101, 102, 103, 104, 105],
    'Department': ['HR', 'Finance', None, 'IT', 'Marketing'],
    'Email': ['a@company.com', None, 'c@company.com', 'd@company.com', 'e@company.com'],
    'Location': ['London', 'New York', 'Berlin', 'Paris', None]
}

df = pd.DataFrame(data)

#Count the missing values in each column

missing_counts = df.isnull().sum()

#Calculate completeness percentage

total_rows = len(df)
completeness_percentage = (1 - missing_counts / total_rows) * 100

```

**Example Output:**

```python

Missing Values:
EmployeeID    0
Department    1
Email         1
Location      1

Completeness (%):
EmployeeID    100.0
Department     80.0
Email          80.0
Location       80.0

```

In this dataset:

* **EmployeeID** is fully complete with no missing values.
* **Department**, **Email**, and **Location** each have one missing entry, leading to an 80% completeness score for those columns.


**How the Completeness Percentage is Calculated**

The formula used is:

```
Completeness = (1 - (Missing Values / Total Records)) × 100
```


#  Duplication Checks in Data Quality

**Duplication** assesses the presence of duplicate or redundant data within a dataset.
A duplicate means the same record (or key attribute) appears more than once, often caused by data entry errors, system glitches, or integration issues.


##  Why Duplicates Are a Problem

* **Data accuracy** – Conflicting copies make it hard to know which record is correct.
* **Storage efficiency** – Extra rows waste space and increase costs.
* **Data integrity** – Duplicates can break relationships in your data model.
* **Efficient processing** – Cleaner data = faster queries and better performance.
* **Reliable analysis** – Duplicates skew metrics, leading to false insights.
* **Cost savings** – Fewer duplicates reduce storage and management overhead.

*Imagine a company with millions of customers—duplicates would quickly multiply storage and complexity!*


## When Duplicates Are Acceptable

In some scenarios, duplicates are intentional because they represent valid repeated events:

| **Scenario**           | **Data Representation**                            |
| ---------------------- | -------------------------------------------------- |
| Customer order history | Multiple rows per customer ID show separate orders |
| Service requests       | Repeated requests tracked over time                |
| Sensor data            | Multiple identical readings over time              |
| Logging & audit trails | Duplicate log entries preserve events              |
| User interaction data  | Repeated interactions are meaningful               |
| Change history         | Duplicates preserve past versions or edits         |

**In these cases, duplicates are by design and support historical tracking or detailed analysis.**

---

##  Code Example: Detecting Duplicate Records

```python
import pandas as pd

# Sample dataset with intentional duplicate EmployeeIDs
data = {
    'EmployeeID': [101, 102, 103, 101, 104, 105, 102],
    'FirstName': ['Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank', 'Bob'],
    'LastName': ['Smith', 'Johnson', 'Brown', 'Davis', 'Lee', 'White', 'Johnson'],
}
df = pd.DataFrame(data)

# Identify duplicates based on EmployeeID
duplicated_mask = df.duplicated(subset='EmployeeID', keep='first')

# Mark duplicates in a new column
df['IsDuplicate'] = duplicated_mask

# Calculate duplicate percentage
duplicate_percentage = (df['IsDuplicate'].sum() / len(df)) * 100

# Display results
print(df)
print(f"Percentage of Duplicate Records: {duplicate_percentage:.2f}%")
```

**Output:**

```
   EmployeeID FirstName LastName  IsDuplicate
0         101     Alice    Smith        False
1         102       Bob  Johnson        False
2         103   Charlie    Brown        False
3         101     David    Davis         True
4         104       Eve      Lee        False
5         105     Frank    White        False
6         102       Bob  Johnson         True

Percentage of Duplicate Records: 28.57%
```


##  Key Takeaways

* **The fewer duplicates, the better!**
* `duplicated(subset=..., keep=...)` is your go-to tool in pandas.
* Always define *which columns* determine duplication (e.g., `EmployeeID`).
* The acceptable level of duplicates depends on your dataset’s purpose and industry standards.

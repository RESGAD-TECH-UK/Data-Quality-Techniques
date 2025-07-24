#  Uniqueness Checks in Data Quality

**Uniqueness** measures the presence of unique values in a dataset.
It helps identify anomalies such as **duplicated keys** or repeated records that should be unique.



##  Code Example: Uniqueness Check on an Email Column

```python
import pandas as pd

#  Create a sample dataset
data = {
    'Email': [
        'john.doe@example.com',
        'jane.smith@example.com',
        'james.doe@example.com',
        'susan.brown@example.com'
    ],
}
df = pd.DataFrame(data)

#  Check uniqueness and create a Boolean mask for duplicated email addresses
duplicated_mask = df['Email'].duplicated(keep='first')

#  Create a new column to indicate uniqueness
df['Uniqueness'] = ~duplicated_mask

#  Calculate uniqueness %
unique_percentage = (df['Uniqueness'].sum() / len(df)) * 100

#  Display results
print("Dataset with Uniqueness Check: ")
print(df)
print(f"Percentage of Unique Records: {unique_percentage:.2f}%")
```

**Output:**

```
Dataset with Uniqueness Check:
                     Email  Uniqueness
0     john.doe@example.com        True
1   jane.smith@example.com        True
2    james.doe@example.com        True
3  susan.brown@example.com        True

Percentage of Unique Records: 100.00%
```

 **All email addresses are unique.**



##  Why Perform Uniqueness Checks?

Uniqueness checks ensure critical identifiers in your dataset are not duplicated.
Here are common fields that should be unique:

* **Customer IDs** – avoid duplicate customer records.
* **Product SKUs** – manage inventory without duplication.
* **Email addresses** – prevent duplicate accounts or duplicate messages.
* **Employee IDs** – distinguish employees in HR systems.
* **Vehicle Identification Numbers (VINs)** – track vehicles uniquely.
* **Barcodes & QR codes** – track products and packages.
* **Usernames / User IDs** – manage user accounts distinctly.
* **Serial Numbers** – identify manufactured items individually.
* **Transaction IDs** – prevent duplicate entries in financial systems.


##  Handling Non‑Unique Records

When non‑unique records are found:

*  **Remove duplicates** if they are exact copies.
*  **Aggregate data** when duplicates carry additional info.
*  **Resolve conflicts** (e.g., merge or update) based on business rules.



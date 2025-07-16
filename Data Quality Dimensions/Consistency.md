# **Consistency in Data Quality**

**Consistency** measures how well data follows established rules, standards, and formats throughout a dataset. It ensures that information can be reliably processed, compared, and interpreted.

When performing consistency checks, you should look for the following:


###  **Key Aspects of Consistency**

**Same Format**
All data should follow the same format, structure, and standards across every record and column.
*Example:* Dates should follow a single format (e.g., `YYYY-MM-DD`), and product IDs should be represented uniformly.

**Adherence to Standards**
Data should align with predefined rules, guidelines, naming conventions, and reference values.
*Example:* If product names must follow a set prefix, all records must reflect that prefix.

**Data Type and Format Validation**
Each field should contain the expected data type (text, number, date) and follow the correct formatting conventions.
*Example:* A numeric field should not contain text values.


### **Practical Example: Checking Consistency in Product Names**

Suppose we have a dataset of products, and our naming convention requires that every `ProductName` begins with the prefix **"PROD"**.


```python
import pandas as pd

# Create the dataset**

data = {
    'ProductID': [1, 2, 3, 4, 5],
    'ProductName': ['PROD001', 'PROD002', 'Product003', 'PROD004', 'PROD005'],
}
df = pd.DataFrame(data)

# Define the expected prefix**

expected_prefix = "PROD"


# dentify inconsistencies
# Check if each product name starts with the expected prefix:


inconsistent_mask = ~df['ProductName'].str.startswith(expected_prefix)
df['Consistency'] = ~inconsistent_mask
```
**Explanation:**

`df['ProductName'].str.startswith(expected_prefix)`
This returns a Boolean Series (True/False for each row):
True if the value in ProductName starts with expected_prefix,
False if it doesn’t.

`~` is the bitwise NOT operator in `pandas/NumPy`, which flips True to False and False to True.

So after applying `~`, you now have:

`True` where the product name does NOT start with the expected prefix.
`False` where it does start with the expected prefix.



```python
# Calculate consistency percentage
consistent_percentage = (df['Consistency'].sum() / len(df)) * 100

# Display results
print("Dataset with Consistency Check:")
print(df)
print(f"Percentage of Consistent Rows: {consistent_percentage:.2f}%")

```



**Example Output:**

```
Dataset with Consistency Check:
   ProductID  ProductName  Consistency
0          1     PROD001         True
1          2     PROD002         True
2          3  Product003        False
3          4     PROD004         True
4          5     PROD005         True

Percentage of Consistent Rows: 80.00%
```

In this dataset, **3 out of 5 product names** follow the expected naming convention, resulting in an **80% consistency rate**.
The entry `Product003` is flagged as inconsistent because it does not begin with the required prefix.



###  **Why This Matters**

Running consistency checks like this:

* Ensures data adheres to business rules and naming standards.
* Makes reporting and downstream analytics more reliable.
* Highlights areas that require data cleansing or process improvement.


# Accuracy
Accuracy measures how much your data agrees with a reliable reference.


## Understanding Data Accuracy in Practice

**Data accuracy** refers to how closely your data reflects the real-world entities or values it represents. In many data-driven tasks, it's critical to ensure that the data collected or transformed remains consistent with a reliable source—also called the **ground truth**.

Let’s walk through a simple Python-based example that evaluates accuracy by comparing two datasets: one containing actual observations and another representing the correct reference values.

### Step-by-Step Example


```python
import pandas as pd
# Observed data
observed = {
    'CustomerID': [1, 2, 3, 4, 5],
    'Purchase': ['Laptop', 'Tablet', 'Phone', 'Laptop', 'Monitor'],
    'Amount': [1200, 400, 650, 1250, 300]
}

# Verified correct data
reference = {
    'CustomerID': [1, 2, 3, 4, 5],
    'Purchase': ['Laptop', 'Tablet', 'Phone', 'Laptop', 'Monitor'],
    'Amount': [1200, 400, 699, 1250, 300]  # Notice the slight difference in one row
}

df_observed = pd.DataFrame(observed)
df_reference = pd.DataFrame(reference)
```

####  Compare the Values

We compare both datasets element-wise to see where they match.

```python
comparison = df_observed == df_reference
```
### Sample Output

```
Comparison:
   Name    Age  Gender  City
0  True   True    True  True
1  True   True    True  True
2  True  False    True  True
3  True   True    True  True
4  True   True    True  True
```
#### Calculate Accuracy per Column

This shows how accurate each field is by calculating the percentage of matching values:

```python
accuracy_percent = comparison.mean() * 100
print("Column Accuracy (%):")
print(accuracy_percent)
```

### Sample Output

```
Column Accuracy (%):
CustomerID    100.0
Purchase      100.0
Amount         80.0
```

This tells us that only the `Amount` column had a mismatch for one record—resulting in 80% accuracy for that column.


##  What Is "Ground Truth"?

"Ground truth" refers to a dataset that is considered correct and reliable, used as a baseline for comparison. How you build or acquire this dataset depends on your role and the type of data you’re working with.

### For Data Engineers:

* Define rules to validate incoming data.
* Generate trusted datasets from historical logs.
* Sample and manually review rows for correctness.

### For Data Analysts:

* Use expert-verified data points.
* Reference known historical data.
* Validate conclusions using survey responses or stakeholder feedback.

### For Machine Learning Practitioners:

* Annotate data manually or with expert support.
* Use benchmark datasets.
* Generate synthetic data with known outcomes for controlled testing.



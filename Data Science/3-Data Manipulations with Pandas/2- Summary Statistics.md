# **Summary Statistics**
Summary statistics are the collection of functions that **condense large datasets into interpretable metrics**. They provide quick insights into the **central tendency, spread, and distribution** of data. In pandas/NumPy, several fundamental functions are used when first exploring a DataFrame or Series , the following are basic functions for performing data exploration when you are first handed the data set.
## 1. **`cumsum()` – Cumulative Sum**
- Returns the running total of values along an axis.
```python
sales["weekly_sales"].cumsum() 
#-> If weekly sales are `[10, 20, 30]`, the result is `[10, 30, 60]`.
```
## 2. **`std()` – Standard Deviation**

- Measures the **spread** of values around the mean.
- A high std → data is widely spread, more details in here [[std]]
- Formula: √(Σ(xᵢ – μ)² / n).
```python
sales["weekly_sales"].std()
# -> If sales are stable, std is small; if they fluctuate, std is large.
```
## 3. **`mean()` – Arithmetic Mean**

- The simple average. Sensitive to outliers.
```python
sales["weekly_sales"].mean()
# -> Example: `[10, 20, 100]` → mean = 43.3, but this hides the spike.
```
## 4. **`median()` – Middle Value**

- Robust measure of the centre.
- Not affected by outliers like the mean.
```python
sales["weekly_sales"].median()
Example: [10, 20, 100] → median = 20.
```
## 5. **`quantile()` – Distribution Cutoffs**
* This function allows for variables of the median , think of it as median is quantile(0.5)
```python
sales["weekly_sales"].quantile([0.25, 0.5, 0.75])
#Example: `[5,10,15,20,25,30,35,40]` →  
#Q1 = 10, Median (Q2) = 20, Q3 = 32.5
```
## Aggregation 
linguistically , to aggregate is to create something formed from the comination and compression of many things , in the context of data *Aggregation* is the process of combining and summarizing many values into a single representation. In the context of pandas, it can be used to:
- Apply **summary statistics** to a column (mean, sum, std, etc.)
- Apply **custom functions** to transform the data into a single value or set of values
In other words the `.agg()` method is used to **aggregate a column**:
- Collapse all values in a column into a single value using a predefined function (e.g., `sum`, `mean`)
- Or apply multiple functions at once by passing a list to `.agg()`

### Example 1: Single aggregation

```python
import pandas as pd

data = pd.DataFrame({
    "sales": [100, 200, 150, 300, 250]
})

# Aggregate using mean
mean_sales = data["sales"].agg("mean")
print(mean_sales)

# output : 200.0
```
### Example 2: Multiple aggregations

```python
summary_sales = data["sales"].agg(["mean", "sum", "max"]) print(summary_sales)`

#Output:
#mean    200.0 sum    1000.0 max     300.0 Name: sales, dtype: float64
```
### Example 3: Custom function

```python
def range_func(x):     
	return x.max() - x.min()  
range_sales = data["sales"].agg(range_func) print(range_sales)

#Output:200
``` 
***
**Remark:** Dates in pandas are stored as the `datetime64` data type. When working with these, you **cannot directly apply numerical operations like `mean()`**, but methods such as `min()` and `max()` are fully supported for finding the earliest or latest dates.

Counting
this section will basically deal with تغربيل a dataset , basically removing duplicates or determing the frequency of a certain value 
to first filter the data fram you can use the method .drop_duplicates("name_of_the_column") , just like in sorting , this method can have multiple arguments thus imposing a priority system 
to assess the frequency of a value in a dataframe you can use the df["name of column"].value_counts() method  you can add to it normalisation to find the proportions of each value in the column via adding normalize=True to the value counts method or sorting by addidng sort= True inside the method too

## Counting

This section focuses on **analyzing a dataset** by either removing duplicates or determining the frequency of certain values.

### Removing duplicates
To filter a DataFrame and remove duplicate rows based on one or more columns, use the `.drop_duplicates()` method. Multiple columns can be passed to impose a **priority system**, similar to sorting[[sorting priority system]]

**Example:**

```python
import pandas as pd

data = {
    "store": ["A", "A", "B", "B", "C"],
    "type": ["X", "X", "Y", "Y", "Z"],
    "sales": [100, 100, 200, 200, 150]
}

df = pd.DataFrame(data)

# Remove duplicate store/type combinations
unique_store_type = df.drop_duplicates(["store", "type"])
print(unique_store_type)
# output :
  store type  sales
0     A    X    100
2     B    Y    200
4     C    Z    150
```

## Counting frequency of values

To determine how often each value appears in a column(s), use the `.value_counts()` method. This is useful for understanding the distribution of categorical data.

**Example for single column :**

```python
import pandas as pd

data = {
    "store": ["A", "A", "B", "B", "C", "A", "B"],
    "sales": [100, 120, 200, 150, 150, 130, 180]
}

df = pd.DataFrame(data)

# Count occurrences of each store
store_counts = df["store"].value_counts()
print(store_counts)
# Output:
# A    3
# B    3
# C    1

# Get proportions instead of raw counts
store_proportions = df["store"].value_counts(normalize=True)
print(store_proportions)
# Output:
# A    0.428571
# B    0.428571
# C    0.142857
````


**Example: for multiple columns**

```python
import pandas as pd

data = {
    "store": ["A", "A", "B", "B", "C", "A", "B"],
    "type": ["X", "Y", "X", "Y", "X", "X", "Y"],
    "sales": [100, 120, 200, 150, 150, 130, 180]
}

df = pd.DataFrame(data)

# Count occurrences of each combination of store and type
combo_counts = df[["store", "type"]].value_counts()
print(combo_counts)
# Output:
# store  type
# A      X       2
# B      Y       2
# B      X       1
# A      Y       1
# C      X       1
# dtype: int64
```

## Grouped Summaries

Grouped summaries involve performing summary statistics on subgroups of a large group that is the column, you can either do this manually or by using the method `df.groupby('column_name')`, pandas automatically partitions the DataFrame into blocks where each block contains rows with the same value in the specified column. You can then compute statistics or apply aggregation functions on these blocks to reveal insights. 
You can also group by multiple columns, which creates a hierarchical structure respecting the priority order of the columns but unlike with duplicates this is only to control the flow not that important , you can reerse the position of arguments and still get the same result.

example for low level no use of groupby func : 
```python
# Calculate total weekly sales
sales_all = sales['weekly_sales'].sum()
# Calculate total weekly sales for type A stores
mask=sales['type']=='A'
sales_A = sales[mask]['weekly_sales'].sum()
# Calculate total weekly sales for type B stores
mask1=sales['type']=='B'
sales_B = sales[mask1]['weekly_sales'].sum()
# Calculate total weekly sales for type C stores
mask2=sales['type']=='C'
sales_C = sales[mask2]['weekly_sales'].sum()
# Create a list of totals for A, B, and C, divide by overall total. Print the result.
sales_propn_by_type = [sales_A,sales_B,sales_C]/sales_all
print(sales_propn_by_type)

# output : [0.9097747 0.0902253 0. ]
```
example of using groupby func
```python
# Group sales by type and calculate total weekly sales
sales_by_type = sales.groupby('type')['weekly_sales'].sum()
# Calculate the proportion of sales at each store type
sales_propn_by_type = sales_by_type/sales['weekly_sales'].sum()
# Print the result
print(sales_propn_by_type)

#output: 
type 
A 0.909775 
B 0.090225
```
.groupby(['type', 'date']) for multiple index

## Pivot Tables

A **pivot table** is a powerful tool for reorganizing and summarizing a DataFrame. It’s conceptually similar to `groupby` but gives more flexibility in how you lay out the results.
```python
import pandas as pd

# Sample data
data = {
    "Department": ["A", "A", "B", "B", "B"],
    "Store": ["X", "Y", "X", "Y", "Z"],
    "Sales": [100, 200, 150, 300, 50]
}

df = pd.DataFrame(data)

# Pivot table with margins
pivot = df.pivot_table(
    values="Sales",
    index="Department", # if multiple ['departement','divison']
    columns="Store",
    aggfunc="mean",
    fill_value=0,
    margins=True
)

print(pivot)

#output :
Store        X      Y   Z   All
Department                     
A          100    200   0  150.0
B          150    300  50  166.7
All        125    250  25  160.0

```
- The **==index==** argument corresponds to the row grouping (like the first argument in `groupby`).
- The **==columns==** argument determines how the data is split into separate columns. This is often for **readability**, as it lets you see multiple dimensions at once. Like `groupby`, you can create multi-level indexes to branch the table hierarchically thus not using the columns thing.
- The **==values==** argument specifies which data is being aggregated (e.g., sales, counts).
- The ==`fill_value`== function is used to replace missing entries with a default value (like 0).
- The ==`margins`== argument adds a row and column labeled `'All'` to show **overall totals or averages**, - notice how the overall `'All'` is **not** simply `(A All + B All)/2 = (150 + 166.7)/2 = 158.35`, which would be the mean of means instead it is rather the Overall mean: You take all the individual values together, ignoring groupings, and compute a single mean ( `(100+150+300+200+50)/5`)
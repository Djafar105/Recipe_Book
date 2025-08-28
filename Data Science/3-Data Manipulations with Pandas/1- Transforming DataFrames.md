# Transforming DataFrames
## Getting to know a DataFrame
### useful commands 
```python
df.head() #returns the first few rows
df.info() #returns general infos like the number of rows and column , column name and data type and how many empty cells are there in each one 
df.shape # returns : (number of rows , number of column)
df.describe() # returns some basic statistcs
```

Pandas are a product of values (2d numpy array) index list and column list 
insert img
```python
df.values # Blue
df.columns # Red
d.index # Green
```

## Adding a New Column in Pandas

You can create a new column in a DataFrame by assigning values directly. The new column can be:
- A constant value  
- Derived from another column  
- Computed from multiple columns  

### Example 1: Assigning a constant value
```python
import pandas as pd

df = pd.DataFrame({
    "state": ["CA", "NV", "TX"],
    "population": [39, 3, 29]
})

# Add a new column with a constant value
df["country"] = "USA"
print(df)

```
# Indexing in Pandas DataFrames

Manipulating the index of a DataFrame can make data access and subsetting more convenient. Here are the key operations:

* **Setting a column as the index**  
  Use `df.set_index("column_name")` to make a column the index of the DataFrame.  
  Example:
  ```python
  import pandas as pd

  data = {
      "City": ["Paris", "London", "Tokyo"],
      "Population": [2148327, 8908081, 13929286]
  }

  df = pd.DataFrame(data)
  df_indexed = df.set_index("City")
  print(df_indexed)
  
  # output : 
         Population
City              
Paris       2148327
London      8908081
Tokyo      13929286
```

## **Resetting the index back to the default integer index**  
Use `df.reset_index()` to revert the index to the default integer index while keeping the current index as a column.  
    Example:
```python
df_reset = df_indexed.reset_index() print(df_reset)
    
# Output:
    City  Population 
0   Paris     2148327 
1  London     8908081 
2   Tokyo    13929286
    ```
## **Dropping the index column entirely when resetting**  
Use `df.reset_index(drop=True)` to remove the current index column completely.  
    Example:
```python
df_reset_drop = df_indexed.reset_index(drop=True) 
print(df_reset_drop)
# Output:
	Population 
0     2148327 
1     8908081 
2    13929286
```
## *Creating a multi-level index**  
* Use a list of column names in `set_index()` to create a hierarchical index.  
```python
  df_multi = df.set_index(["Country", "City"])
  print(df_multi)
  # output : 
                  Population
Country City              
France  Paris       2148327
        Lyon         515695
Japan   Tokyo      13929286
        Osaka       2691186
```

## **Accessing data with a multi-level index**  
### Isolating ONE row or column
You can select rows or columns at any level using `.loc[]`.  
Example: Get all cities in France:
```python
print(df_multi.loc["France",:])
# Output:
       Population
City             
Paris    2148327
Lyon      515695
 ```

To access a specific **inner level** under a particular outer level, pass a tuple[[tuple]]:
```python
df_multi.loc[("Japan", "Tokyo"),:]
# Output:
Population    13929286
Name: (Japan, Tokyo), dtype: int64
```

### Isolating multiple rows or columns : slicing 
slicing multiple outer levels:
```python
df_multi.loc["France":"Japan",:]
# Output:
               Population
Country City             
France  Paris      2148327
        Lyon        515695
Japan   Tokyo     13929286
        Osaka      2691186
```
slicing multiple inner levels:
Selecting **specific points** ==>use **tuples inside a list**:
```python
df.loc[[("France","Paris"), ("Japan","Tokyo")],:]
#output:
               Population
Country City             
France  Paris     2148327
Japan   Tokyo    13929286
```

Select a range of cities under `France`:
```python 
df_multi.loc[("France", "Lyon"):("France", "Paris"),:] #rq : - Outer level must be specified in the tuple !

#Output:
               Population
Country City             
France  Lyon       515695
        Marseille  861635
        Paris     2148327
```
***
- You can sort a DataFrame by its index using:
```python
df.sort_index(level='x')  # x is the name of the index level to sort by eg: 'city' or 'country'
```
- If you plan to slice rows using `.loc[]`, **the index must be sorted** first to preserve meaning

## Manipulating Dates in DataFrames
- When working with dates, you can slice by a specific period, e.g., the 2000s, directly.
```python
subset_2000s = temperatures.loc['2000-01-01':'2009-12-31']
```
- Dates should follow the **ISO 8601 format**: `"yyyy-mm-dd"` for proper sorting and slicing.
- **Filtering by year, month, or day using `.dt`:**
```python   
 temperatures.drop_duplicates('date').dt.year   ❌  
 temperatures['date'].drop_duplicates().dt.year   ✅
```
- **Extracting month or day:**
```python
# Extract month from the 'date' column 
temperatures['date'].dt.month  
# Extract day from the 'date' column 
temperatures['date'].dt.day`
```
- **Notes:**
    * Make sure you're working with a Series, not a DataFrame bedause `.dt` accessor works **only on Series** with dtype `datetime64`. thus we got the error above

when calculating the mean , you can specefiy wether you want it by row or by column , by specifying the axis= 'index' or 'columns'
weird behavior : i have a problem in a pivot table when i do the mean func , and i specify the axis to columns it does the index and when i do the index it does the column , weird bahvior also when i dont specify the axis it does the columns per defeault #weird 
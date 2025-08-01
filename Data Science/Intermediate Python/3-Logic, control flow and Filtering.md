# Logic, control flow and Filtering
## Boolean Operators
* Numpy : 
	* in numpy you can subset using boolean filters [[4-Numpy#^978431]] but if you want to apply multiple logic checks at a time you need to use other nupy functions like :
	```python
		 logical_and()
		 logical_or()
		 logical_not()
	```
	* example : `array_name[np.logical.and(insert the logical operation here)` : this would allow you to create another array containing the elements that only verify the logical filtering done 
	* We don’t necessarily need to use `np.logical_*` functions (like `np.logical_and`) directly for subsetting. In fact, we almost never apply them as part of the slicing itself. Their main role is to **generate a boolean mask** that can then be used in standard subsetting operations.  
	* When working with multiple arrays, you can’t subset them all at once using a single `np.logical_*` call. Instead, you use these functions to build a logical filter (a boolean array), and then apply this mask individually to each array using the usual indexing syntax (e.g., `array[mask]`).
	*  **Example**
	
	```python
	import numpy as np
	
	my_house = np.array([18.0, 20.0, 10.75, 9.50])
	your_house = np.array([14.0, 24.0, 14.25, 9.0])
	
	# Create a mask where both arrays have values < 15
	mask = np.logical_and(my_house < 15, your_house < 15)
	
	print(mask)               # Output: [False False  True  True]
	print(my_house[mask])     # Subset of my_house
	print(your_house[mask])   # Subset of your_house
	```

## Filtiring Pandas DataFrames

* Whether in pandas or NumPy, logic-based advanced filtering generally involves three steps.  
* ***First**, for 2D structures (like DataFrames or 2D arrays), you may need to extract the specific **range of data** (rows or columns) on which the filtering will be applied. This step isn’t necessary for 1D arrays or Series.  
* ***Second**, you run a logical condition on that data range, which produces a **filter** (or mask). This filter is simply a boolean structure (`True` or `False` for each element) indicating which elements satisfy the condition.  
* ***Third**, you apply this filter as an index in a **basic slicing** operation to retrieve only the elements where the mask is `True`.  

 **Example with NumPy**
```python
import numpy as np
arr = np.array([2, 5, 8, 1, 10])
filter = arr > 5           # Step 2: create a boolean filter
print(arr[filter])         # Step 3: apply filter -> [ 8 10 ]
```

 **Example with pandas (Single Condition)**
```python
import pandas as pd
df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 17, 35]
})
filter = df["age"] > 18    # Step 2: boolean mask on 'age'
print(df[filter])          # Step 3: subset rows where age > 18
```

**Example with pandas (Multiple Conditions using np.logical_and)**
```python
import numpy as np

# Use np.logical_and to combine conditions
filter = np.logical_and(df["age"] > 18, df["age"] < 30)
print(df[filter])    # Rows where 18 < age < 30
```
* In both pandas and NumPy, the syntax and logic are almost identical — the filter (mask) is what drives the selection.  
* For multiple conditions, `np.logical_and` or `np.logical_or` is often used.

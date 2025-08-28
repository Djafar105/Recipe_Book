# Loops
## While Loops in Python  

While loops are less common than `for` loops for simple iteration, but they remain **essential in scenarios where the number of iterations is not predetermined**, such as in **machine learning model refinement** (e.g., repeatedly training until the error rate falls below a threshold (initial value of a variable)).  

The **basic concept** of a `while` loop is that a condition (a logical check) is evaluated **before each iteration**.  
- **Crucial rule:** The variable controlling the condition must be updated within the loop body, or you risk creating an infinite loop.  

### **Example**
```python
# Example: Reduce error until threshold is reached
error = 10
while error > 1:
    print("Current error:"error)
    error -= 2  # Update the condition variable
print("Error below threshold!")
```
In this example, the loop continues running as long as `error > 1`. By decrementing `error` in each iteration, the condition will eventually fail, preventing an infinite loop.
***
***
## For Loops – The Automated Slicer/Seasoner  

A `for` loop in Python works like an **automated slicer/seasoner**: it takes each "slice" (element) from a structure like a list, one by one, and "seasons" it by applying a specific recipe (the code block). Once it's done with one slice, it automatically moves to the next until no elements remain.  

### **Example with a List**
```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:  # 'fruit' takes each element in order
    print("Making juice with",fruit)
```
**Output:**
```
Making juice with apple
Making juice with banana
Making juice with cherry
```
Here, the loop variable `fruit` is not an index; it is directly assigned each element of the list during the slicing process.

---

* ### **Using `range()` – Automated Counter**  
When you don’t have a list but want to repeat an action a fixed number of times, `range()` acts as an **automated counter** that generates numbers on the fly.

### **Example with `range()`**
```python
for i in range(3):  # i takes the values 0, 1, 2
    print("Step",i)
```
**Output:**
```
Step 0
Step 1
Step 2
```
*** 
* ### enumerate() 
	* It allows you to loop over a list (or iterable) while also getting the index (position) of each element.
	* It automatically generates pairs (index, value) during each iteration. the first variable in the unpacking (e.g., x) will hold the index, and the second (e.g., height) will hold the element value.
```python
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
for x, height in enumerate(areas):
    print(x, height)
```
-------------------------------
```python
Output:
0 11.25
1 18.0
2 20.0
3 10.75
4 9.5
```

***
***
## Loop Data Structures
Looping over other data structures like arrays, DataFrames, and dictionaries follows the same general logic as looping over lists, but the way we access elements changes. For **dictionaries**, we use two iterator variables — by convention order 1 :`key` and order 2 :`value` — and call the `.items()` method to retrieve key-value pairs during iteration:  
```python
my_dict = {"a": 1, "b": 2}
for bi, boo in my_dict.items():
    print(bi, boo)
```
**Output:**  
```
a 1
b 2
```

For **NumPy arrays**, a 1D array can be iterated like a list, but for **2D arrays**, if you want to iterate element by element, you need to use the `np.nditer()` function:  
```python
import numpy as np
arr = np.array([[1, 2], [3, 4]])
for x in np.nditer(arr):
    print(x)
```
**Output:**  
```
1
2
3
4
```

Note that for dictionaries we use a **method** (`.items()`), while for NumPy arrays we use a **function** (`np.nditer()`).
### For Loops with DataFrames  

When you loop over a DataFrame directly (e.g., `for x in dataframe:`), you will only get the **column names**, not the rows. To access the data row by row, you use the `iterrows()` method, which yields a pair `(label, row)` for each row. The first variable stores the index label, and the second is a Series representing the row data.

### **Example – Iterating Rows**
```python
import pandas as pd

df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 35]
})

for label, row in df.iterrows():
    print(f"Index: {label}, Name: {row['name']}, Age: {row['age']}")
```
**Output:**
```
Index: 0, Name: Alice, Age: 25
Index: 1, Name: Bob, Age: 30
Index: 2, Name: Charlie, Age: 35
```

---

### **Adding a New Column with a Loop**
You can add a new column by assigning values during iteration:  
```python
df['age_plus_10'] = 0  # Initialize column
for label, row in df.iterrows():
    df.loc[label, 'age_plus_10'] = row['age'] + 10
```

---

### **Using `apply()` Instead of Loops**
A more efficient approach is to use `apply()`, which applies a function to each element of a column:  
```python
df['age_plus_10'] = df['age'].apply(lambda x: x + 10)
```
This avoids explicit row-by-row looping and is faster for large datasets.

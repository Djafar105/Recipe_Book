# Numpy 
## Introduction : 
* **NumPy (Numeric Python)** is a package that introduces a new, faster, and more efficient way to manipulate lists. By using its core `array()` function (the star of the show), you transform a list into a **mathematical object** optimized for elegant, complex, and vectorized numeric operations.
***
## array() :
### Introduction :
- The array function, unlike lists, can only contain one type of elements
- array is considered an independent python type , so it has methods as well that behaves in a particular manner
### NumPy Subsetting

^978431

- NumPy introduces **logic-based (boolean) subsetting**, a powerful alternative to traditional index-based selection.
    
- When you apply a **logical condition** to an array (e.g., `bmi > 14`), NumPy returns a **boolean array** where each element corresponds to whether the condition is `True` or `False`.
    
- You can then use this boolean array as a hook to filter and bring back desired elements directly: `array_name[array_name > 14]` returns only the values that satisfy the condition.
    
- **Example:** `
	* `bmi = np.array([10, 15, 12, 14, 16, 18])
	* `bmi > 14 --> Output: array([False,  True, False, False,  True,  True])
	* `bmi[bmi > 14] --> Output: array([15, 16, 18])`
***
## 2D NumPy Arrays

**Attributes vs Methods**
- Before starting, there is the concept of an **attribute**, which looks syntactically similar to a method (`.method()`) but is different.
- An **attribute** gives information about the object and is accessed as `.attribute` (no parentheses).
- **Example:** `array_name.shape` → returns the shape (format) of the array.

**What is a 2D Array?**
* A 2D array is essentially a **matrix** with rows and columns, supporting a wide range of manipulations.
    - In syntax, a 2D array is created by turning a nested list into an array using `numpy.array()`.
    - Each inner list is now treated as a **row**, and each position across rows forms a **column**.
    - Once inside a NumPy array, these are no longer "sublists" but part of one unified structure — a single array formed by rows and columns.

**Homogeneity of Elements**
*  A NumPy array can only hold **one data type** (`dtype`).
*  If one element is turned into a string, all elements are converted to strings for consistency, **as strings take priority.**
    
**Subsetting**  
* can be same as nested lists [[2-Python Lists#^b10872]] or actually in a new intuitive way : 
	* `name_of_array[index of the row , index of the column ]`
* you can select mini 2d arrays , sth that is not really easily possible in nested lists[[2-Python Lists#^6fc1f9]], via basically slicing by fixing the range index for both the row and column argument 
* example: `name_of_array[4:7,1:3]`: this would basically allow to :
	* fix the rows : 4,5and6 
	* fix the columns : 1and 2 
	* crossing them and the crossed results in an array 
* you can select all the columns or all the rows via simply : 
	* `name_of_array[row_index, :]`
	* `name_of_array[:, column_index]`
***
## NumPy: Basic Statistics
- numpy package contains also functions that allow for basic statistical operations on your arrays , these function can serve as a sanity check , on of the first steps when treating your big set of data 
- examples : 
	- `numpy.mean(name_of_array)or(name_of_array[....])`
	- `numpy.median(name_of_array)or(name_of_array[....])
	- `numpy.std(name_of_array)or(name_of_array[....])`: std for sexually transmitted diseases
	* `numpy.corrcoef(name_of_array[....])`

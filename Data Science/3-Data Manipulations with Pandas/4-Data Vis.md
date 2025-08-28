## 🥑 Avocado Data Visualization fundamentals in Python

This block demonstrates several useful plotting techniques using `matplotlib` and `pandas` with avocado sales data: 
### Bar :
a bar plot is not a curve variable as it does not describe evolution but rather categorical distribution of things. think of it as controlled bins distribution: the number of bins and the name of each one is specified and so the value to each bin
```python
df['column'].plot(kind='bar')
#or 
plt.bar(df)
```

### Rot : 
For better readability you can rotate the indexes on the axis 
```python
avocados['type'].value_counts().plot(kind='bar', rot=45)
```

### Superpose, Invisibility and Legending
For direct comparision and exposure to plots you can choose to plot on top of each another by not clearing the canvas , and you can control the invisibility by the alpha argument and finally you can give them legends to which one is which 
```python 
avocados[avocados['type'] == 'conventional']['avg_price'].hist(alpha=0.5)
avocados[avocados['type'] == 'organic']['avg_price'].hist(alpha=0.5)
plt.legend(["Conventional", "Organic"])
```
### Clarification about .plot and plt
In plotting we can use **Pandas’ `.plot()`** without explicitly importing `matplotlib.pyplot`, but advanced customization (titles, axis labels, legends, layout) are more controlled with the  `plt`.  
- **Pandas `.plot(kind=...)`** → high-level (fast) wrapper around Matplotlib.
    - Easier, faster, works directly on Series/DataFrames.
- **Matplotlib `plt.plot()`** → low-level, defaults to **line plots**, no `kind` argument.
    - More control and flexibility, but rigid and takes effort.
examples : 
1- **Using Pandas only** (no `plt`):
```python
# Line plot with kind argument
avocados['avg_price'].plot(kind='line', title="Avg price over index")

# Scatter plot with x and y
avocados.plot(x='nb_sold', y='avg_price', kind='scatter', title="Sales vs. Price")
```
2- **Using Matplotlib directly**:
```python
plt.plot(avocados['avg_price'])  # defaults to line plot
plt.title("Avg price over index (Matplotlib)")
plt.xlabel("Index")
plt.ylabel("Avg Price")
plt.show()
```
3- **Mixed use** (Pandas for quick plot + Matplotlib for customization):
```python
ax = avocados.plot(x='nb_sold', y='avg_price', kind='scatter')
plt.title("Sales vs. Price")
plt.xlabel("Number of Avocados Sold")
plt.ylabel("Average Price")
plt.show()
```
 
***
## Handling Missing Values in Pandas
### First exposure to missing values 
**Missing entries** in a DataFrame are represented as `NaN` (Not a Number) ,  to reveal if a value is qualified as mising or not you can run a mask on the totality of the dataframe and returns a boolean dataframe 
### Example :
```python
df = pd.DataFrame({
    "SampleID": ["A001", "A002", "A003", "A004"],
    "ProteinConcentration": [2.5, 'NaN', 3.1, 'Nan'],
    "TimePoint": [0, 5, 'NaN', 10]
})
df.isna()
#output : 
   SampleID  ProteinConcentration  TimePoint
0     False                 False      False
1     False                  True      False
2     False                 False       True
3     False                  True      False
```
### Second exposure 
you can proceed after the mask to actually aggregate each column into a one boolean value representing wether a column contains at least one NaN and then to a value revealing the number of the NaN present in a column
### Example 
```python
# First chzck if there is any 
df.isna().any()
#output : 
SampleID              False
ProteinConcentration   True
TimePoint              True
dtype: bool

# second check the number of missing values
df.isna().sum()
#output :
SampleID               0
ProteinConcentration   2
TimePoint              1
dtype: int64
```
### Dropping & Replacing Missing Values
* When we discover a missing value we can either choose to eliminate the whole row (dropping ) or to replace it with a desired value
### Example 
```python 
# Dropping 
df.dropna()
# output :
  SampleID  ProteinConcentration  TimePoint
0     A001                  2.5        0.0

# Replacing 
df.fillna(0)
# Output :
  SampleID  ProteinConcentration  TimePoint
0     A001                  2.5        0.0
1     A002                  0.0        5.0
2     A003                  3.1        0.0
3     A004                  0.0       10.0
```
***
## Creating DataFrames from Dictionaries
* you can either create dataframes by assembling multiple dictionaries ina list then convert it to df
example :
```python
# Create a list of dictionaries with new data
avocados_list = [
    {
        'date':"2019-11-03",
        'small_sold':10376832,
        'large_sold':7835071,
    },
    {
        'date':"2019-11-10",
        'small_sold':10717154,
        'large_sold':8561348,
    }
]
# Convert the list into a DataFrame
avocados_2019 = pd.DataFrame(avocados_list)
# Print avocados_2019
print(avocados_2019)
#output: 
	date small_sold large_sold 
0 2019-11-03 10376832 7835071 
1 2019-11-10 10717154 8561348
```
* You can directly convert a dictionary into a DataFrame. Conceptually, this involves organizing data by assigning all values corresponding to a given key made into a list.
### Example 
```python
# Create a dictionary of lists with the new avocado data

avocados_dict = {
    'date':["2019-11-17","2019-12-01"],
    'small_sold':[10859987,9291631],
    'large_sold':[7674135,6238096]
}
# Convert the dictionary to a DataFrame
avocados_2019 = pd.DataFrame(avocados_dict)
# Print the DataFrame
print(avocados_2019)
#output :
	date small_sold large_sold 
0 2019-11-17 10859987 7674135 
1 2019-12-01 9291631 6238096
```
***
## CSV

**CSV (Comma-Separated Values)** is a simple, widely used **file format** for storing tabular data. Each line represents a row, and columns are separated by commas. It’s a common way to exchange data between tools, especially in data science, bioinformatics, and spreadsheet applications.
### Example CSV Content
```csv
SampleID,ProteinConcentration,TimePoint
A001,2.5,0
A002,3.1,5
A003,2.8,10

```
### Turn a CSV into a DataFrame
```python
airline_bumping = pd.read_csv("path/to/csv")
```

### Turn a dataframe into CSV
```python 
airline_totals_sorted.to_csv('airline_totals_sorted.csv', index=False)
```

***
> The  .groupby results in a serie not dataframe
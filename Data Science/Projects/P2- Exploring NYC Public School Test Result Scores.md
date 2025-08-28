## Context : 
Every year, American high school students take SATs, which are standardized tests intended to measure literacy, numeracy, and writing skills. There are three sections - reading, math, and writing, each with a **maximum score of 800 points**. These tests are extremely important for students and colleges, as they play a pivotal role in the admissions process.

Analyzing the performance of schools is important for a variety of stakeholders, including policy and education professionals, researchers, government, and even parents considering which school their children should attend.

You have been provided with a dataset called `schools.csv`, which is previewed below.

You have been tasked with answering three key questions about New York City (NYC) public school SAT performance.

***
## Instructions :
Which NYC schools have the best math results?

- The best math results are at least 80% of the ***maximum possible score of 800*** for math.
- Save your results in a pandas DataFrame called `best_math_schools`, including `"school_name"` and `"average_math"` columns, sorted by `"average_math"` in descending order.

What are the top 10 performing schools based on the combined SAT scores?

- Save your results as a pandas DataFrame called `top_10_schools` containing the `"school_name"` and a new column named `"total_SAT"`, with results ordered by `"total_SAT"` in descending order (`"total_SAT"` being the sum of math, reading, and writing scores).

Which single borough has the largest standard deviation in the combined SAT score?

- Save your results as a pandas DataFrame called `largest_std_dev`.
- The DataFrame should contain one row, with:
    - `"borough"` - the name of the NYC borough with the largest standard deviation of `"total_SAT"`.
    - `"num_schools"` - the number of schools in the borough.
    - `"average_SAT"` - the mean of `"total_SAT"`.
    - `"std_SAT"` - the standard deviation of `"total_SAT"`.
- Round all numeric values to two decimal places.

***
## Code :
```python
import pandas as pd 
schools = pd.read_csv("schools.csv")
# task 1
mask1=schools['average_math']>=640
best_math_schools=schools[mask1][['school_name','average_math']].sort_values('average_math',ascending=False)
print(best_math_schools)
# task 2
piv=schools.pivot_table(
    index='school_name',
    values=['average_math','average_reading','average_writing']
).sum(axis=1).sort_values(ascending=False)
tot_sat=piv.reset_index()
tot_sat = tot_sat.rename(columns={0:'total_SAT'})
top_10_schools=tot_sat.iloc[0:10,:]
print(top_10_schools)
#i wonder if i can do it with directly dataframe or groupby
piv2=schools.pivot_table(
    index=['borough','school_name'],
    values=['average_math','average_reading','average_writing']
).sum(axis=1)#.sort_index(ascending=False)
tot_sat_bor=piv2.reset_index()
tot_sat_bor = tot_sat_bor.rename(columns={0:'total_SAT'})
largest_std_devi= tot_sat_bor.groupby('borough')['total_SAT'].agg(['mean','std']).sort_values('std',ascending=False).round(2)
#print(largest_std_devi) : just to verify 
largest_std_dev=largest_std_devi.reset_index().iloc[[0],:]
largest_std_dev['num_schools']=len(schools[schools['borough']==largest_std_dev['borough'].values[0]]) 
# Extracting a scalar (the borough name) with .iloc[0] avoids index mismatch — pandas compares Series to scalar safely.  
# Comparing two Series with different indexes triggers an error due to ambiguous alignment.which is our case thus we need to do the extraction using .values[0]
#largest_std_dev=largest_std_dev.rename(columns={['mean','std']:['average_SAT','std_SAT']}) : error cuz the rename()needs a dictionnary
largest_std_dev = largest_std_dev.rename(columns={'mean': 'average_SAT', 'std': 'std_SAT'})

print(largest_std_dev)
```

## Output : 
![Pasted image 20250826123415.png](./images/Pasted%20image%2020250826123415.png)
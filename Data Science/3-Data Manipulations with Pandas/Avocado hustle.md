# Avocado hustle
```python
# the goal is to plot the avocade consumption in function of dates for both types organic and conventional using three methods , dataframes , groupby and pivot tables

#avocados is loaded
# dataframes :
import matplotlib.pyplot as plt 

mask1= avocados['type']=='organic'
mask2= avocados['type']=='conventional'
organic_sub_dataframe=avocados[mask1]
conventional_sub_dataframe=avocados[mask2]


#organic plot

#x_axis_O = organic_sub_dataframe['date']
#y_axis_O = organic_sub_dataframe['nb_sold']
#plt.plot(x_axis_O,y_axis_O)
        # when we did this we got multiple curves leading us to discovering that a data value can repeat thus we needed to aggregate the values of date and nb_sold :

# Step 1: Group by date and sum nb_sold
aggregated_O = organic_sub_dataframe.groupby('date')['nb_sold'].sum()

unique_dates_O = aggregated_O.index
total_nb_sold_O = aggregated_O.values

plt.plot(unique_dates_O,total_nb_sold_O)

#conventional plot
aggregated_C = conventional_sub_dataframe.groupby('date')['nb_sold'].sum()
unique_dates_C = aggregated_C.index
total_nb_sold_C = aggregated_C.values

plt.plot(unique_dates_C,total_nb_sold_C)
plt.show()







#groupby
avocados_grp=avocados.groupby(['type','date'])['nb_sold'].sum()
dates_O=avocados_grp[avocados_grp.index.get_level_values('type')=='organic'].index.get_level_values('date')
nb_sold_O=avocados_grp[avocados_grp.index.get_level_values('type')=='organic'].values
plt.plot(dates_O,nb_sold_O)


dates_C=avocados_grp[avocados_grp.index.get_level_values('type')=='conventional'].index.get_level_values('date')
nb_sold_C=avocados_grp[avocados_grp.index.get_level_values('type')=='conventional'].values
plt.plot(dates_C,nb_sold_C)

plt.show()




#pivot_table

#avocados_pivtab=avocados.pivot_table(index='type',columns=['date','nb_sold'],values=avocados_pivtab.columns.sum()) : tried to time travel here

#setting up the pivot table
avocados_pivtab=avocados.pivot_table(index='type',columns='date',values='nb_sold',aggfunc='sum') # the aggfunc is so magical it works even if we swap the index and columns

#organic
dates_O=avocados_pivtab[avocados_pivtab.index=='organic'].columns
nb_sold_O=avocados_pivtab[avocados_pivtab.index=='organic'].values.flatten() # so apparently the values in a pivot table are numpy arrays of 2 dimension even if it is one row thus needs flattening , weird , needs more investigation 
plt.plot(dates_O,nb_sold_O)


#conventional
dates_C=avocados_pivtab[avocados_pivtab.index=='conventional'].columns
nb_sold_C=avocados_pivtab[avocados_pivtab.index=='conventional'].values.flatten()
plt.plot(dates_C,nb_sold_C)

plt.show()
```

![Capture d'écran 2025-08-25 160521.png](./images/Capture%20d%27%C3%A9cran%202025-08-25%20160521.png)
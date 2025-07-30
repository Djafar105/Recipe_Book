## Context
**Netflix**! What started in 1997 as a DVD rental service has since exploded into one of the largest entertainment and media companies.

Given the large number of movies and series available on the platform, it is a perfect opportunity to flex your exploratory data analysis skills and dive into the entertainment industry.

You work for a production company that specializes in nostalgic styles. You want to do some research on movies released in the 1990's. You'll delve into Netflix data and perform exploratory data analysis to better understand this awesome movie decade!

You have been supplied with the dataset `netflix_data.csv`, along with the following table detailing the column names and descriptions. Feel free to experiment further after submitting!
***
Perform exploratory data analysis on the `netflix_data.csv` data to understand more about movies from the 1990s decade.

- What was the most frequent **movie** duration in the 1990s? Save an approximate answer as an integer called `duration` (use 1990 as the decade's start year).
    
- A movie is considered short if it is less than 90 minutes. Count the number of **short action movies** released in the 1990s and save this integer as `short_movie_count`.
    

Feel free to experiment after submitting the project!
***

## Code 
```python
import pandas as pd
import matplotlib.pyplot as plt
netflix_df = pd.read_csv("netflix_data.csv")
#print(netflix_df) # just wanted to see 
filter = netflix_df['type'] == 'Movie'
movies_only = netflix_df[filter]
filter1 = np.logical_and(movies_only['release_year']>1990,movies_only['release_year']<1999)
movies_only_1990s= movies_only[filter1]
#print(movies_only_1990s['release_year']) : just to verify
#print(movies_only_1990s['type']): just to verify
duration=round(movies_only_1990s['duration'].mean())
print("The frequent movie duration during the 1990s is around: ",duration,"mins")

#filter2 = netflix_df['genre'] == 'Short Movies'
#short_movies = netflix_df[filter2]
#print(netflix_df['genre'].unique()) : did this to actually findout and understand that there is no short movie genre and i need to create it 
filter2 = movies_only_1990s['genre'] == 'Action'
action_movies = movies_only_1990s[filter2]
#print(action_movies) : just to verify
filter3= action_movies['duration'] < 90
short_movie_count=len(action_movies[filter3])
#print(short_movie_count['duration']) : just to verify
#print("During the 1990s, there are around: ",short_movie_count,"short action movies")
```
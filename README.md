# Final-Project-Statistical-Modelling-with-Python

## Project/Goals 
The goal with this project was to be able to explore the structure of specific API's, query them and understand the data returned. I chose So-Bi, a bike sharing entity in Hamilton, Ontario and enlisted the help of both the Foursquare and Yelp API's to gather information on various POI's, as well as their ratings and reviews.I anticipated a strong correlation between the utilization rate and the bike station location.  


## Process 
##### 1. Accessed city bikes API to gather relevant information for all of the bike stations in the city of Hamilton. 
##### 2. Used the API to call the latitude, longitude and number of bikes.
##### 3. Used the latitude and longitude acquired in step 2 to use the YELP API to call up to 20 results for all restaurants, bars and parks within a 1000m radius.
##### 4. Used the latitude and longitude acquired in step 2 to use the YELP API to call results for nearby places
##### 5. Parsed all of the data to create data frames and saved as separate .csv files.
##### 6. Employed Seaborn to help plot the data on various graphs to see what would be the best representative.
##### 7. Merged the data from a few of the .csv files to use for my regression model. 


## Results 
When trying to compare Yelp with Foursquare, I personally found Yelp easier to use and more informative. I feel that ratings and reviews are good indicators of potential interest and customer engagment given the demographic of where the most bikes were being used, which was near McMaster University. My regression model did show a high R-squared value however it also indicated that there could be a multicollinearity that needs to be further reviewed. 

```python
import pandas as pd
import statsmodels.api as sm

df = pd.read_excel('merged_data_all.xlsx')  

df['utilization_rate'] = df['empty_slots'] / df['total_spots']

X = df[['Available Bikes', 'empty_slots', 'rating', 'review_count']]
y = df['utilization_rate']

X = sm.add_constant(X)

model = sm.OLS(y, X).fit()

print(model.summary())
```



## Challenges  
### The challenges I faced in the project were as follows:
 - There was not enough time to choose the optimal date and time for the data we were expected to collect. While data was still produced, more interesting data could be grabbed if say we were able to look at past data or not be restricted to the current season (winter).
 - The time it took to navigate the different nuances between foursquare and yelp compromised the time that could have been spent diving further in or collecting more data.
 - It was difficult for me to get good graphical representation due to what I believe was the results of using a reduced dataset. While there was 145 stations in total, I decided to only use the top 10 stations with the most bikes.


## Future Goals 
If I had more time, I would collect data over a longer time period and explore all of the bike stations for So-bi to get a more comprehensive view. I believe this would help me test out additional hypothesis' With additional time, there would also be the option to make more calls to the API's not risking going over the daily limit that Yelp imposed. 

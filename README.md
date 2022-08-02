# MY PARENTS KICKED ME OUT! Where do I go now?

### Final materials are located in the [Consolidated_new folder](/Consolidated_new).
### Final presentation is located in the [Presentation folder](/Presentation).
### Draft materials are located in the [Draft folder](/Draft).


## Table of Contents

* [Background Story](#background-story)
* [Data Team](#data-team)
* [Inital Data Exploration & Gathering](#initial-data-exploration-and-data-gathering)
* [Analysis](#analysis)
* [Conclusion](#conclusion)
* [Reference](#references) 



## Background Story:  

In our latest "Ask the Data Experts" blog, we received the following question from Paul, who just got kicked out of his parent's house in Decatur, Georgia:

> "Having spent many years with my parents, they finally decided to kick me out! :worried: But where do I go now? Do I stay in Georgia or move to another State? Should I look for a studio or a 1 bedroom apartment? Would you all be able to use data to help me with some recommendations?" - Paul (29 years old)

When digging further into Paul's preferences, he mentioned the following:
- Affordability is important.
- Wants to have space.
- Open to living with or without roomates.
- Most of his friends and family live in Georgia, but he's open to moving to another state if needed.
- Wants to feel safe
- Paul is a homebody - but he wants to make sure there's things to do whenever he feels like getting out of the house! 



## Data Team: 

To help answer Paul's question, we've assembled a team of 9 of our best data experts:
- Maheen Abdulwaheed
- Huda Alghazouli 
- Andres Almaraz
- Gautam Iyer
- William M Mills
- Ashley Moore
- Sarje Page
- Vinika Patel
- Sheyla Perez Nazco



## Initial Data Exploration and Data Gathering: 

Our initial data exploration phase started by exploring some of the data sets available on the United States' Office of Policy Development and Research [website](https://www.huduser.gov/portal/about/mission_and_background.html). 

In this website, we were able to find the following [data sets](https://www.huduser.gov/portal/datasets/50per.html#2022), which contain median rent estimates for all of the different counties in the United States (and its territories). The rent estimates are for studios, 1 bedrooms, 2 bedrooms, 3 bedrooms and 4 bedrooms. 

Since we wanted to give Paul the most up to date information, we focused on 2020-2022 data. We saved the different csv files (2020, 2021, 2022) in the following [folder](/Consolidated_new/UTF/). 



## Analysis

## Setting Up the Data

The first step that we took in our [Jupyter Notebook](/Consolidated_new/Project_Group_7.ipynb) was to read the 3 different CSV files (2020-2022):

- `rents_2020 = pd.read_csv("UTF/FY2020_50_County_rev.csv")`
- `rents_2021 = pd.read_csv("UTF/FY2021_50_County.csv")`
- `rents_2022 = pd.read_csv("UTF/FY2022_FMR_50_county_rev.csv")`

We were then able to merge the 3 CSVs files into one DataFrame by merging 2020 with 2021, and then merging 2020-2021 with 2022:
- `rent_20_21_22 = pd.merge(rent_20_21, rents_2022, how="left", on=["state", "county", "cousub"])`

We also loaded the following [file](/Consolidated_new/Other_Files/rent.csv), which contains the same data but formatted in a different way. We converted this DataFrame into a new summary DF (rent_summary_sy), which groups the average rents by state and year. This will be used later in the analysis to calculate the YoY % change in rent.



## Data Cleaning

After merging the data, we reduced the DataFrame to only the necessary columns, renamed the columns, and dropped null values from the data. 

After we cleaned our data, we were left with the following 20 columns:
- **state**  →  displays state ID 
- **county**  →  displays county ID
- **county name**  →  displays name of the county
- **state initial**  →  displays initial of the state (e.g. TX stands for Texas)
- **studio_2020**  →  median rent price for a studio in 2020
- **studio_2021**  →  median rent price for a studio in 2021
- **studio_2021**  →  median rent price for a studio in 2022
- **bedroom_1_2020**  →  median rent price for a 1 bedroom in 2020
- **bedroom_1_2021**  →  median rent price for a 1 bedroom in 2021
- **bedroom_1_2022**  →  median rent price for a 1 bedroom in 2022
- **bedroom_2_2020**  →   rent price for a 2 bedroom in 2020
- **bedroom_2_2021**  →  median rent price for a 2 bedroom in 2021
- **bedroom_2_2022**  →  median rent price for a 2 bedroom in 2022
- **bedroom_3_2020**  →  median rent price for a 3 bedroom in 2020
- **bedroom_3_2021**  →   rent price for a 3 bedroom in 2021
- **bedroom_3_2022**  →  median rent price for a 3 bedroom in 2022
- **bedroom_4_2020**  →  median rent price for a 4 bedroom in 2020
- **bedroom_4_2021**  →  median rent price for a 4 bedroom in 2021
- **bedroom_4_2022**  →  median rent price for a 4 bedroom in 2022
- **pop_2017** ->  county population (as of 2017)

Our new cleaned DataFrame was exported into a csv [file](/Consolidated_new/Merged_Data/rent20-22.csv):
- `cleaned_rent_20_21_22.to_csv("Merged_Data/rent20-22.csv")`



## **Question 1)** If Paul decides to live alone, should he go for a studio or a one bedroom apartment?

The first question that we wanted to help Paul with was whether he should go for a studio or one bedroom apartment. We know that affordability is important to Paul, but he also wants to live comfortable, is it worth it to get a one bedroom apartment?

In order to help answer this question, we calculated the average rent per number of bedrooms, focusing on 2021 data, and created a bar plot: 

![image](/Consolidated_new/Screenshots/Screenshot%201.png)

    As expected, the average rent for a one bedroom is more expensive than a studio apartment. However, the increase in rent is only 10%. 

## **Question 2)** Shoud Paul Consider Living with Roommates? 

For question 2, we loaded a csv [file](/Consolidated_new/Other_Files/Rent%20Based%20on%20Distance.csv) that contains the average rents per state by room size (studio, 1 bedroom, 2 bedroom, 3 bedroom, 4 bedroom). 

We made a scatter plot that shows that living with a roommate would be cheaper for Paul than living alone. This is true across all states:

![image](/Consolidated_new/Screenshots/Screenshot%2022.png)

If Paul is willing, getting a 4 bedroom with 3 roommmates would be the most cost-effective option:

![image](/Consolidated_new/Screenshots/Screenshot%2023.png)


## **Question 3)** What is the variability in rent prices for the different bedroom types (studio, 1, 2, 3 or 4 bedroom)? 

We were also curious about the variability of the different bedroom types. Is there more variability in 4 bedrooms compared to 1 bedrooms? 

To answer this question, we created a boxplot that shows rent price for each number of bedrooms:

![image](/Consolidated_new/Screenshots/Screenshot%202.png)

    Based on the boxplots, studios and 1 bedrooms have less variability in rent prices. 4 bedrooms have the highest variability. 


### **First Recommendation**: After talking with Paul, he's decided to live alone. We recommend a 1 bedroom apartment, as there is only a 10% difference in rent between a studio and a one bedroom apartment. This will help Paul have more space. 

### We'll be mostly focusing on 1 bedroom rent prices for the rest of the analysis. 


## **Question 4)** How have rent prices changed per state YoY? (% Increase)

Since we want to ensure that Paul moves to an affordable state, we analyzed how rent prices had changed YoY (2020 vs. 2021) for 1 bedrooms across each of the states. We visualized this using a bar plot:

![image](/Consolidated_new/Screenshots/Screenshot%203.png)

    From 2020 to 2021, the majority of states experienced a YoY increase in rent prices, with the exception of AK, SD, VT, 
    WV and WY. California and Rhode  Island had the biggest YoY increase in rent, indicating that these wouldn't be good 
    options for Paul if affordability is very important. While Georgia's rent prices also increased YoY, they did so a 
    slower pace than many other states. 



## **Question 5)** What are the top 5 most expensive states by rent price? What are the top 5 least expensive states by rent price? 

While YoY changes in rent prices are important, we also checked which states were the most and least affordable. We created an average rent for all of the different bedroom types and figured out the 5 most expensive and 5 least expensive states (using groupby functions).  

Top 5 Most Expensive States by Rent Price:

![image](/Consolidated_new/Screenshots/Screenshot%204.png)

    Hawaii, DC, Massachussets, California and New Jersey were the 5 most expensive states based on rent estimates for 2021. 

Top 5 Most Affordable States by Rent Price:

![image](/Consolidated_new/Screenshots/Screenshot%205.png)

    Puerto Rico, Arkansas, Mississipi, Missouri and Kentucky were the least 5 expensive states based on rent estimates for 2021.

We also wanted to plot the most and least expensive states for 1 bedrooms into a heatmap. We imported a [file](/Consolidated_new/Other_Files/state_coordinates.csv) containing the different coordinates (lat, lng) for each of the states. We merged the coordinates with the state DataFrame and used the gmaps API.

Top 5 Most Expensive States Plotted on Heatmap:

![image](/Consolidated_new/Screenshots/Screenshot%207.png)

Top 5 Most Affordable States Plotted on Heatmap:

![image](/Consolidated_new/Screenshots/Screenshot%208.png)



### **Second Recommendation**: After following up with Paul and enlightening him about Georgia's rent prices not being in the top 5 states. We suggested that he stay in Georgia. He took our recommendation and decided to stay close to his family and friends in GA.



## **Question 6)** Within Georgia, what are the rent prices of 1 bedrooms for each of the different counties? 

Georgia has 156 counties, a lot of information for just one chart. Therefore, we created 3 different bar charts, organized into alphabetical order.

Median 1 Bedroom Rent for the First 50 Counties (Appling to Echols County):

![image](/Consolidated_new/Screenshots/Screenshot%209.png)

Median 1 Bedroom Rent for the Second 50 Counties (Effingham to Mitchell County):

![image](/Consolidated_new/Screenshots/Screenshot%2010.png)

Median 1 Bedroom Rent for the Last 56 Counties (Montgomery to Worth County):

![image](/Consolidated_new/Screenshots/Screenshot%2011.png)

Based on the bar charts above, there are some counties that may not be suitable for Paul (e.g. Fulton) as they have a high median rent price for 1 bedrooms.



## **Question 7)** What is the correlation between population and rent prices in Georgia counties? 

Population is also an important factor, as Paul is young and wants to live in a place where there's things to do. If he goes to a highly populated city, will rent prices be higher? Is there a correlation between rent prices and correlation?

To answer this question, we created a scatter plot with a regression line that looks at the 1 bedroom rents for 2021 vs. the population size of each GA county:

![image](/Consolidated_new/Screenshots/Screenshot%2012.png)

    Based on the scatter plot, there is a positive correlation between bedroom rent prices and the population of each county. 
    A county with higher population might have higher rent prices.
    
In order to plot a heatmap for the GA counties, we needed to figure out the latitude and longitude of each county. To accomplished this, we loaded this [file](/Consolidated_new/Other_Files/list-counties-georgia.csv), which contains the county seats for each of the GA counties. We used the county seats information to make a call to the google maps [api](https://developers.google.com/maps) and added the latitudes and longitudes of each GA county into our DataFrame:

![image](/Consolidated_new/Screenshots/Screenshot%2021.png)

With the lat and lng information, we created a HeatMap based on the population of each GA county, and added clickable markers showing the highest and lowest counties pased on population size:

![image](/Consolidated_new/Screenshots/Screenshot%2013.png)

    Based on the map, the top 5 counties with the highest population are Cobb, Fulton, DeKalb, Gwinnett and Taliaferro 
    counties. The counties with the least population are Glascock, Chatham, Quitman, Webster and Clay counties. With the 
    exception of Savannah, it looks like the most populated counties are the ones closest to the city of Atlanta. We know 
    that there is a positive correlation between population and rent price. Is there also a correlation between distance 
    from the center of Atlanta and rent price?



## **Question 8)** What is the correlation between distance from the center of Atlanta and rent prices? 

To answer this, we made another call to the gmaps API and calculated the distance of each county from the center of Atlanta:

![image](/Consolidated_new/Screenshots/Code%20Snippet%201.png)

The DataFrame that we created is exported in this [csv](/Consolidated_new/Other_Files/Rent%20Based%20on%20Distance.csv):

![image](/Consolidated_new/Screenshots/Screenshot%20csv.png)

We then created a scatter plot with a regression line that shows the correlation between distance from the center of Atlanta and rent price for a 1 bedroom in 2021:

![image](/Consolidated_new/Screenshots/Screenshot%2014.png)

    Based on the scatter plot, there is a negative correlation between the distance from the center of Atlanta and the rent 
    prices. For the most part, counties that are farther away from Atlanta have lower rent prices. 

We also created bins based on the distance from Atlanta to show some other visualizations that further prove the correlation:

![image](/Consolidated_new/Screenshots/Screenshot%2015.png)

    The boxplots show that the bins closest to Atlanta (<30 and 30-60) have the highest median rent price. We also see a high 
    median rent price around 240-270 miles away from Atlanta, which is where Savannah is located (but the rent is still lower 
    than living in Atlanta). 


![image](/Consolidated_new/Screenshots/Screenshot%2016.png)

    This bar plot further confirms the relationship between distance from Atlanta and rent price, which is seen across all 
    bedroom types (not just one bedrooms!)



## **Question 9)**  Is there a correlation between crime rate and distance from Atlanta?

To answer this question, we loaded a csv [file](/Consolidated_new/Other_Files/Crime_data_per_county.csv) that contains the crime rates (per 1,000) for each of the GA counties and merged it with our GA counties DataFrame. 

Then, we created a scatter plot with a linear regression line showing the correlation between distance from Atlanta and crime rate:

![image](/Consolidated_new/Screenshots/Screenshot%2017.png)

    Based on the scatter plot, it seems like there's no correlation (weak) between the crime rates and the distance from 
    Atlanta! Since the distance does not matter, we would have to look at the crime rates in the counties where Paul is 
    interested to move. 


### **Third Recommendation**: Based on all of the data that we showed to Paul, we've come up with a list of 5 counties that would be good options for Paul to move to.
- ### Coweta County
- ### Chatham County
- ### Cherokee County
- ### Carroll County
- ### Columbia County

These counties were selected because they are close to major cities (Savannah, Atlanta, Augusta), but are not in the heart of Atlanta (Fulton County), which might be more expensive based on our findings. 



## **Question 10)** What are the crime rates for each of the different GA counties that Paul is interested in? 

Below is a DF with the crime rates for each of the 5 counties:

![image](/Consolidated_new/Screenshots/Screenshot%2018.png)

    Based on this, Columbia County has the lowest crime rate (0.97) and the lowest 1 bedroom price as well. 


## **Question 11)** Can we locate leasing offices for each of the counties on Google maps?

In order to further help Paul, we also located different leasing offices that Paul could reach out to in case he wants more information. We accomplished this by using the google places [api](https://developers.google.com/maps/documentation/places/web-service/overview).

Below is a heatmap with markers for each of the leasing offices that we located:

![image](/Consolidated_new/Screenshots/Screenshot%2020.png)



## Conclusion

From the data collected, cleaned, merged and calculated based on States, counties, distance, crime rates and rents, we conclude that the best place for Paul to live in and move to is **Columbia County**. The rent for 1 bedroom apartment is affordable as compared to the other counties and it is the safest place to live in as compared to the other counties that Paul selected. 
 
Columbia county has a lot of things to do outdoors like rock climbing, kayaking, water sports, golf, horseback riding and many parks for hiking. It is close to Augusta too which would be a nice weekend trip for Paul to enjoy. 



## References
- US Department of Housing and Urban Development (2022). 50TH PERCENTILE RENT ESTIMATES 2019-2022. Retrieved July 21, 2022, from https://www.huduser.gov/portal/datasets/50per.html#2022
- Google Developers (2012, January 20). Public Data - States. Retrieved July 21, 2022, from https://developers.google.com/public-data/docs/canonical/states_csv
- List of Georgia Counties with County Seats (2014). Retrieved July 26,2022, from https://www.downloadexcelfiles.com/ge_en/download-excel-file-list-counties-georgia#.YuhfpOzMKw4
- Georgia Bureau of Investigation (2022, March 2). 2020 Summary Report Uniform Crime Reporting (UCR) Program Georgia Crime Information Center. Retrieved July 21, 2022, from https://gbi.georgia.gov/services/crime-statistics
- ASQ.org (2022). Nominal Group Technique. Retrieved July 21, 2022, from https://asq.org/quality-resources/nominal-group-technique#:~:text=Nominal%20group%20technique%20(NGT)%20is,idea%20they%20feel%20is%20best.

# Cyclistic Bike-Share Data Analysis Case Study 

Anna Madsen   
May 2026 

**Context**: This case study was completed through the Coursera Data Analytics Certificate and is centered around providing marketing insights to Cyclistic, a fictional bike-share company based out of Chicago. 

## Introduction: 

Cyclistic is a bike share company in Chicago that provides nearly 6000 bikes and 600 docking stations throughout the city. Both classic and electric bikes are offered, along with other disability-friendly options. Cyclistic offers various tiers of pricing plans: single-ride passes, full-day passes and annual memberships. Casual riders are those who use the single ride and full day passes, and members are those who have an annual membership. Through financial analysis, it has been found that annual members bring in more profit to the company than casual riders. Thus, the company has a goal to maximize the number of annual members by converting casual riders into members through marketing strategies. 

The marketing team would like more insight into this by understanding how annual members and casual riders use the bikes differently, why casual riders would convert to annual memberships and how the company can use digital media to influence casual riders to become members. These insights will help to shape the marketing teams’ strategy to convert casual riders into members in order to maximize annual members and drive more profit. 

## Business Problem: 

The goal of the business is to create a marketing strategy to convert casual riders to members in order to maximize the number of annual members. This analysis will examine historical bike-share data in order to understand how annual members and casual riders use Cyclistic bikes differently. This will help the marketing team better understand the reasons a user chooses to be a casual rider or a member and how to best market towards casual riders to convert them to members. 

## Data Sources: 

This dataset was provided under a license by Motivate International Inc. via Divvy bike sharing service in Chicago, operated by Lyft.   
The dataset contains the last 12 months of ride data, from March 2025-March 2026, and includes the ride ID, bike type, and information on each ride, including the start and end times, start and end stations, and rider type.   
This dataset is representative of bike rides in the last year in Chicago and was provided directly from Divvy via the City of Chicago. This data is suitable for analyzing patterns in how members and casual riders use Cyclistic.   
A limitation of this data is the lack of personally identifiable information due its public nature. Due to this, demographic and residency details, purchase and membership history, and ride history are unavailable for this analysis. 

## Data Cleaning & Preparation: 

This dataset was prepared and cleaned in Python to ensure accuracy, clarity, and usability for analysis. This included consolidating the data, verifying and converting data types, creating new variables, checking consistency and removing erroneous or unnecessary data fields.

**Data Consolidation:**

* 12 monthly datasets were imported and column consistency was verified to ensure stackability   
* Concatenated the 12 datasets to create one full year dataset covering April 2025-March 2026 

**Data Type Conversion & Feature Engineering** 

* Converted timestamp fields to datetime format  
* Created ride length variable from start and end timestamps and verified in timedelta format.   
* Converted ride length to minutes and rounded for readability  
* Created new columns including day of the week, start date, end date, ride month and year and route name (start station \+ end station)

**Data Validation**

* Verified correct data type for key variables including ride length, ride ID, member and bike types, and timestamps   
* Confirmed no duplicate values for ride ID or duplicate rows in entire table   
* Verified consistent ID length for all ride IDs and no missing values for key data variables including ride ID, ride type, ride length and member type   
* Validated values in rideable type, member type, year, month and day of week 

**Missing Data Handling**

* Checked for missing values and identified nulls in station/location fields  
* Replaced nulls with “NO DATA”   
* Retained records as these data fields are not essential for analysis

**Data Cleaning and Filtering** 

* Checked for and removed 29 records with negative ride lengths as these indicate end time occurring before start time, suggesting system or data entry errors   
* Reviewed ride length distribution using upper and lower quantiles. Identified that 99% of rides were under 89.5 minutes and 1% of rides were shorter than 0.26 mins, indicating the presence of extreme high and low outliers.   
* Applied an upper cutoff of greater than 3 hours and a lower cutoff of less than half a minute. This filters out extreme outliers and likely invalid or negligible rides (test unlocks or system errors). 

**Dataset Formatting** 

* Renamed column names for clarity including member column to member type and added units to ride length column name. Renamed rideable type to bike type.   
* Dropped latitude and longitude columns and several other columns used for cleaning as these were not needed for analysis. 

**Final Dataset Summary**

| Initial dataset size  | 5,620,544 | Percent of original dataset |
| :---- | :---- | :---- |
| **Negative trip durations** | 29 | \<0.00% |
| **Short rides \<0.5 min** | 108,759  | 1.94% |
| **Long rides \>3 hrs**  | 16,726 | 0.30% |
| **Total Removed** | 125,514 | 2.23% |
| **Final dataset size**  | 5,495,030 | 97.8% |

* Final dataset includes ride ID, bike type, timestamps, station info, member type, ride length, and time-based ride data.   
* To ensure filtering did not introduce bias, verified representation of both rider groups:

|  | Pre-Clean | Post-Clean |
| :---- | :---- | :---- |
| **Members** | 3,605,045 (64.1%) | 3,547,953 (64.6%) |
| **Casual**  | 2,015,499 (35.9%) | 1,947,077 (35.4%) |


  * Proportion of each rider type in the dataset remained consistent, indicating that filtering did not introduce bias or disproportionately affect either group. 

*Cleaning and data preparation was completed in Python \- full code available in linked repository.* 

## 

## Analysis 

This dataset was analyzed in Python to gain insight into usage differences between casual riders and annual members of Cyclistic bike-share. Metrics analyzed include bike type; ride length and frequency; usage patterns over time of day, days of the week, and weekdays versus weekend; and seasonal usage patterns. Analysis was conducted via grouped aggregations and descriptive statistics. 

* Conducted descriptive analysis on overall ride length statistics    
* Compared ride frequency and average ride length between rider types   
* Analyzed bike type usage between rider types   
* Analyzed relationships between bike type and ride frequency/length across rider types   
* Examined usage patterns based on time of day (morning, afternoon, evening and night)  
* Analyzed usage patterns over days of the week   
* Compared weekday vs weekend usage patterns  
* Analyzed seasonal usage patterns over months of the year across rider types 

*Analysis was completed in Python \- full code available in linked repository.* 

## 

## 

## Key Insights 

1. Overall, annual members ride 82% more, but casual riders take 55% longer trips on average. 

2. Annual members ride 32% more per day on weekdays, while casual riders shift 48% more of their trips to weekends.  
     
 


   

   

   

   

 


   

   

   

   

   

 


3. Members ride consistently throughout the day, with use dropping at night, and take 42% more morning rides than casual users. Casual riders’ usage is concentrated in the afternoon and evening, and ride 73% more at night than members.   
   

4. Usage for both rider types peaks in the summer. However, casual members increase their trip duration in the summer, while members ride relatively the same duration throughout the entire year.   
 


 


   

   

   

   

   

   

   

   

   

   

   

   

   

   

   

 


5. Both rider types show a similar preference for electric bikes. However, casual riders ride significantly longer on classic bikes than on electric (72% more, 25 vs. 15 minutes) where members ride an equal duration on both bike types (11-13mins).   
   

### **Summary**: 

These insights suggest that members use both bike types for functionality and for shorter, consistent, daily routine trips during the week, such as for commuting and errands. On the other hand, casual riders take longer, less frequent, leisure-oriented trips, concentrated on weekends, evenings, and in summer months, and choose classic bikes for longer trips. 

## Recommendations 

Based on these insights, the following marketing strategies and further research are recommended for conversion of casual riders to annual members. 

1. Casual riders do not use bikes as frequently for routine tasks. Cyclistic should promote biking to casual riders as an inexpensive and convenient means of transportation. After 10 rides, a notification should show the cost difference between their rides and gas, and then show savings if they purchase a membership.  
2. Casual riders take longer, infrequent trips in summer months. Cyclistic should run a discounted membership rate for May-August to encourage routine riding during the summer.   
3. Casual riders tend to take longer trips on classic bikes, but use electric bikes more frequently for shorter trips. Cyclistic should promote electric bikes as eco-friendly car replacements and reward riders with eco-conscious badges for extended e-bike usage; riders who are members can redeem these for rewards.   
4. Casual riders ride for leisure rather than routine exercise. Cyclistic should add a feature to their app that tracks miles ridden and calories burned. After a certain number of miles ridden, a discount on membership is offered.     
5. Casual riders ride more at night and weekends than members. Cyclistic should offer a ride bundle for a month of weekend night rides that can be applied to a membership.    
6. Cyclistic should complete further analysis on the proportion of casual riders that live in Chicago vs. tourists to better understand who to target and how these subsets of riders use bikes differently.   
7. Further analysis could explore differences in start and end stations and routes between user types to better clarify use cases. Supplementary data may be needed due to missing station data in the current dataset. 


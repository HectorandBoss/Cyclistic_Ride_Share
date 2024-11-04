# Cyclistic Ride Share

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning And Preparation](#data-cleaning-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Learning Points](#learning-points)
- [Optimization Comparison](#optimization-comparison)

## Project Overview

In this case study, we aim to find out how casual users of cyclistic differ from annual subscribers in terms of usage. Findings from this case study will be used to address the need for a more targeted advertisement approach in the future aimed at turning casual users into annual subscribers which will prop up cyclistic’s profit margin.

### Data Sources

The data sources used for this analysis are "202310-divvy-tripdata.csv",  "202310-divvy-tripdata.csv",  "202311-divvy-tripdata.csv",  "202312-divvy-tripdata.csv",  "202401-divvy-tripdata.csv",  "202402-divvy-tripdata.csv",  "202403-divvy-tripdata.csv",  "202404-divvy-tripdata.csv",  "202405-divvy-tripdata.csv",  "202406-divvy-tripdata.csv",  "202407-divvy-tripdata.csv",  "202408-divvy-tripdata.csv", in the zip file from the source. Each containing monthly data of cyclistic bike usage.

Source: [Download here](https://divvy-tripdata.s3.amazonaws.com/index.html)

### Tools

- R - Data Cleaning, Data Analysis
- Google Docs - Reporting
- Goolgle Slide - Presentation
- Tableau - Dashboard Visualization

### Data Cleaning And Preparation

In the initial data preparation stage, I performed the folliwing tasks:
1. Data extraction into Rstudio from twelve .csv files.
2. Removal of unnecessary fields from each data frame
3. Conversion of supposed Date fields to Date format.
4. Merging all data frames into a new data frame.
5. Creating calculated fields to make data easily accessible for analysis.
6. All rows containing ride duration less than or equal to zero were removed from the data frame.
7. Ordering the data frame by month and day of week for accurate time series plotting.
8. Creating a season field to help find more insights.

### Exploratory Data Analysis

EDA involved exploring the ride share data to answer key questions, such as:

1. What is the user base like?
2. What is the bike usage like for each user type?
3. What is the bike type preference for each user type?
4. what is the average ride duration by each user?
5. What is the average ride duration in each month by each user type?
6. What is the average ride duration by weekday segmented by each user type?
7. What is the average ride duration by hour segmented by each user type?

### Data Analysis

R Script:
```{R}
#package installation
install.packages(c("tidyverse","here","skimr","janitor","data.table","collapse","openxlsx"))

#library initiation
library(tidyverse)
library(readxl)
library(here)
library(skimr)
library(janitor)
library(data.table)
library(collapse)
library(openxlsx)

#data importation
mn_1 <- fread("202310-divvy-tripdata.csv")
mn_2 <- fread("202311-divvy-tripdata.csv")
mn_3 <- fread("202312-divvy-tripdata.csv")
mn_4 <- fread("202401-divvy-tripdata.csv")
mn_5 <- fread("202402-divvy-tripdata.csv")
mn_6 <- fread("202403-divvy-tripdata.csv")
mn_7 <- fread("202404-divvy-tripdata.csv")
mn_8 <- fread("202405-divvy-tripdata.csv")
mn_9 <- fread("202406-divvy-tripdata.csv")
mn_10 <- fread("202407-divvy-tripdata.csv")
mn_11 <- fread("202408-divvy-tripdata.csv")
mn_12 <- fread("202409-divvy-tripdata.csv")

#for our analysis we only need: ride_id, rideable_type, stated_at, ended_at, member_casual
#data cleaning & manipulation -removed unnecessary and incomplete columns
mn_12_v2 <- mn_12 %>% select(-c(start_station_name, 
                                start_station_id, 
                                end_station_name, 
                                end_station_id, 
                                start_lat,
                                start_lng,
                                end_lat,
                                end_lng
                                )
                             )
mn_11_v2 <- mn_11 %>% select(-c(start_station_name, 
                                start_station_id, 
                                end_station_name, 
                                end_station_id, 
                                start_lat,
                                start_lng,
                                end_lat,
                                end_lng
                                )
                             )
mn_10_v2 <- mn_10 %>% select(-c(start_station_name, 
                                start_station_id, 
                                end_station_name, 
                                end_station_id, 
                                start_lat,
                                start_lng,
                                end_lat,
                                end_lng
                                )
                             )
mn_9_v2 <- mn_9 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_8_v2 <- mn_8 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_7_v2 <- mn_7 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_6_v2 <- mn_6 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_5_v2 <- mn_5 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_4_v2 <- mn_4 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_3_v2 <- mn_3 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_2_v2 <- mn_2 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )
mn_1_v2 <- mn_1 %>% select(-c(start_station_name, 
                              start_station_id, 
                              end_station_name, 
                              end_station_id, 
                              start_lat,
                              start_lng,
                              end_lat,
                              end_lng
                              )
                           )

#skim_without_charts showed that moments were added to time in the last 4 months
#& electric_scotter was just introduced in mn_12


#data aggregation -one table for all data needed 
all_trips <- bind_rows(mn_1_v2, 
                       mn_2_v2, 
                       mn_3_v2,
                       mn_4_v2,
                       mn_5_v2,
                       mn_6_v2,
                       mn_7_v2,
                       mn_8_v2,
                       mn_9_v2,
                       mn_10_v2,
                       mn_11_v2,
                       mn_12_v2
                       )

#data processing (generating calculated field)
#turning date column into different time periods
all_trips <- mutate(all_trips,
                    month = format(as.Date(started_at), "%B"),
                    day = format(as.Date(started_at), "%d"),
                    year = format(as.Date(started_at), "%Y"),
                    day_of_week = format(as.Date(started_at), "%A"),
                    time_of_day = format(as.POSIXct(started_at), "%H")
                    )
#getting ride duration field
all_trips[, ride_length_min := difftime(ended_at, started_at, units = "mins")]
all_trips$ride_length_min <- as.numeric(all_trips$ride_length_min, units = "mins")
#removing rows where the bike wasn't driven by users
all_trips_v2 <- all_trips[ride_length_min > 0]

#ordering fields for easy understanding
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, 
                                    levels=c("Sunday", "Monday", 
                                             "Tuesday", "Wednesday", 
                                             "Thursday", "Friday", 
                                             "Saturday"
                                            )
                                  )
all_trips_v2$month <- ordered(all_trips_v2$month, 
                              levels=c("January", "February", 
                                       "March", "April", 
                                       "May", "June", 
                                       "July", "August",
                                       "September", "October",
                                       "November", "December"
                                      )
                              )
#adding seasons field
all_trips_v2 <- all_trips_v2 %>%
  mutate(
    season = case_when(
      month %in% c("December", "January", "February") ~ "Winter",
      month %in% c("March", "April", "May") ~ "Spring",
      month %in% c("June", "July", "August") ~ "Summer",
      month %in% c("September", "October", "November")
      ~ "Autumn",
      TRUE ~ "Unknown"  # Handle unexpected values
    )
  )

#descriptive analysis to help in further analysis and visualization
#below shows that with casuals cover longer distances relative to members though their smaller population
print(all_trips_v2[, .(
  mean_ride_length = fmean(ride_length_min),
  median_ride_length = fmedian(ride_length_min),
  max_ride_length = fmax(ride_length_min),
  min_ride_length = fmin(ride_length_min)
), by = member_casual])
print(table(all_trips_v2$member_casual)) #plot member vs casual


#Visualization for clarity
#1. members unlock and dock bikes almost double that of casuals -flexing unlimited pass (business knowledge)
ggplot(all_trips) + 
  geom_bar(aes(x = member_casual, fill = member_casual)) +
  xlab("User Type") +
  ylab("Total No. of Use") +
  ggtitle("The Impact of Membership on Usage Frequency") 

#2. rideable_type isn't a factor for determining usage time or user_type
ggplot(all_trips_v2,aes(rideable_type)) + 
  geom_bar(aes(fill = member_casual)) + 
  facet_wrap(~member_casual) +
  xlab("Bike Type") +
  ylab("Total No. of Use") +
  ggtitle("Bike Type Preference by Membership Status")

#3
ggplot(all_trips, aes(member_casual)) +
  geom_bar(aes(fill = member_casual)) +
  xlab("User Type") +
  ylab("Amount of users") +
  ggtitle("User Distribution by Membership Type")



#segmenting data for easy visualization
mean_monthly_trips <- all_trips_v2[, .(mean_ride_length = fmean(ride_length_min)), by = .(member_casual, month)]
mean_daily_trips <- all_trips_v2[, .(mean_ride_length = fmean(ride_length_min)), by = .(member_casual, day_of_week)]
mean_hourly_trips <- all_trips_v2[, .(mean_ride_length = fmean(ride_length_min)), by = .(member_casual, time_of_day)]

#4. casuals use their bikes longer than members
ggplot(mean_daily_trips) + 
  geom_col(aes(member_casual, 
               mean_ride_length, 
               fill = member_casual)) +
  xlab("User Type") +
  ylab("Average Ride Duration (Min)") +
  ggtitle("Average Ride Duration By User Type")


#monthly usage mean
#5. peak usage month: may - august
ggplot(mean_monthly_trips, aes(month,mean_ride_length)) +
  geom_col(aes(fill = member_casual)) +
  theme(aspect.ratio = 0.3) +
  xlab("Month") +
  ylab("Average Ride Duration (Min)") +
  ggtitle("Average Ride Duration By Month") +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1))

#6. mean daily usage
#peak usage days: casuals Fri Sat, Sun -could it be for shopping?
ggplot(mean_daily_trips,aes(day_of_week, mean_ride_length)) + 
  geom_col(aes(fill = member_casual)) +
  theme(aspect.ratio = 0.3) +
  xlab("Day") +
  ylab("Average Ride Duration (Min)") +
  ggtitle("Average Ride Duration By Day")

#7. mean hourly usage
#peak usage hours: 
ggplot(mean_hourly_trips,aes(time_of_day, mean_ride_length)) + 
  geom_col(aes(fill = member_casual)) +
  theme(aspect.ratio = 0.4) +
  xlab("Hour") +
  ylab("Average Ride Duration (Min)") +
  ggtitle("Average Ride Duration By Time of Day")

#Export Data for further analysis and visualization
fwrite(all_trips_v2, file = "all_trips.csv")
fwrite(mean_monthly_trips, file = "mean_monthly_trips.csv")
fwrite(mean_daily_trips, file = "mean_daily_trips.csv")
```

### Results
The analysis results are summarized below:

1. 'Members' are almost double the number of 'Casuals'.
2. 'Members' use bikes for less time than 'casuals' per ride.
3. `Bike_type` is not a factor in determining usage.
4. 'Casuals' use bikes for longer time period per ride than 'members'.
5. Summer months have the highest biking activity.
6. Weekends have the highest biking activity led by 'Casuals'.
7. Inconclusive result, as there is no pattern in biking activity when segmented into hours.
8. On work days, 'Members' have a constant average ride duration, showing that members are mostly working class or students.
9.  From friday to sunday, biking activities increases led by 'casuals' showing that all both user types are interested in leisure activities like shopping, exercising, e.t.c.

Clean Data for visualization: 'mean_monthly_trips.csv', 'mean_daily_trips.csv', 'mean_hourly_trips.csv'.

### Recommendations

My recommendations from the analysis are:
- Reduce membership single ride time to 30 minutes from 45 minutes for work days but 45min on weekends with reduced price.
- Redeemable Loyalty points for members: LP redemption for coffee, bottle water, giftcards or coupon, cyclistic merchandise, spotify discount.
- Craft promotions that showcase what ‘casuals’ are missing out on to promote membership.
- Slight price increase on weekends and summer time on single_pass sales.

### Limitations

I had to remove the `start_station_name`, `start_station_id`, `end_station_name`, `end_station_id` fields as the last four datasets had alot of missing values in those fields there by causing bias as fields for more than a quarter was empty.

I also removed rows where the ride duration were less than 1 minute as it could be seen as bike re-docking or staff running maintainance check.

### Learning Points

1. I learnt to optimize my script by using better packages, below is a comparison between my initial script processing profile and an optimized version which is what I used in this doocumentation.
2. I learnt to use github as it has always seem overwhelming in previous times.
3. I learnt to never rush through the data cleaning phase of any project.
4. I mastered the use of 'ggplot' for data visualization in R.

### Optimization Comparison

Initial script runtime: 1,041,780 ms ~ 17 Min 21 sec

Optimized script runtime: 193,800 ms ~ 3 Min 13 sec

Time saved: 14 Min 8 sec

Initial Script Profiling:

![unoptimized profvis](unoptimized%20profvis.PNG)

Optimized Script Profiling:

![optimized profvis](Optimized%20profvis.PNG)


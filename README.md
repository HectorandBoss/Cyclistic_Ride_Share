# Cyclistic Ride Share

## Project Overview

In this case study, we aim to find out how casual users of cyclistic differ from annual subscribers in terms of usage. Findings from this case study will be used to address the need for a more targeted advertisement approach in the future aimed at turning casual users into annual subscribers which will prop up cyclistic’s profit margin.

### Data Sources

The data sources used for this analysis are "202310-divvy-tripdata.csv",  "202310-divvy-tripdata.csv",  "202311-divvy-tripdata.csv",  "202312-divvy-tripdata.csv",  "202401-divvy-tripdata.csv",  "202402-divvy-tripdata.csv",  "202403-divvy-tripdata.csv",  "202404-divvy-tripdata.csv",  "202405-divvy-tripdata.csv",  "202406-divvy-tripdata.csv",  "202407-divvy-tripdata.csv",  "202408-divvy-tripdata.csv", each containing monthly data of cyclistic bike usage.

### Tools

- R - Data Cleaning, Data Analysis
- Google Docs - Reporting
- Goolgle Slide - Presentation
- Tableau - Dashboard Visualization

### Data Cleaning & Preparation

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

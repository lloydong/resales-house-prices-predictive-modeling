
# HDB Resale Prices Predictive Modeling

![HDB](./pictures/cover_pics.webp "HDB")

## Project Overview

The HDB resale market in Singapore has become highly competitive, characterized by increasing demand and fluctuating pricing trends. WOW!, a top-tier real estate agency in Singapore, aims to equip its agents with a powerful, data-driven tool to:

- Provide clients with expert pricing advice for buying or selling HDB resale flats in a dynamic market.
- Precisely estimate the value of HDB resale flats across various flat types and locations.

In response to this, the CEO has tasked the Head of the Data Analytics Team with analyzing the HDB resale market and developing an advanced predictive model to deliver accurate insights in a short turnaround time.

## Table of Contents
1. [Problem Definition](#problem-definition)
2. [Data Collection](#data-collection)
3. [Data Exploration](#data-exploration)
4. [Data Cleaning](#data-cleaning)
5. [Analysis](#analysis)
6. [Modeling (if applicable)](#modeling)
7. [Results and Insights](#results-and-insights)
8. [Conclusion](#conclusion)
9. [Future Work](#future-work)

## Problem Definition
- Problem Statement
  - Develop a linear regression model to accurately predict the value of HDB resale flats, taking into account various flat types and locations. Additionally, create an interactive dashboard that allows users to easily access and visualize these property valuations.
    
- Audiences
  - CEO of WOW! 


## Data Collection
- **Dataset Overview**:
  - GA's ‘train_data.csv’, 78 columns x 150,634 rows, January 2012 to April 2021
  - GA's ‘test_data.csv’, 78 columns x 16,737 rows, March 2012 to April 2021
- **Data Description**: Floor Level, Unit Type, HDB Age, Location, Approximate distance to Public Transport/Hawker Center/etc.

## Data Limitations
- **Limited training data**: Only from March to June 201
- **Historical biases**: E.g., during economic downturns or periods of low demand can skew predictions
- **Macroeconomic events**: Factors like oil price changes, pandemics, or geopolitical instability (e.g., wars, government regulations) can drastically alter flight pricing

## Data Cleaning
- **Missing Values**: Replaced with '0' for mall within 500km, 1km and 2km and for hawker within 500m, 1km and 2km that have null values
- **Remove data**: Dropped 829 data  for 'mall nearest distance'
- **Duplicates**: No duplicate rows 
- **Data Transformation**: Converted data to the correct format
  
## Analysis
- **Feature Engineering**:
  -	Created ‘region’ from ‘town’ which has 'south', 'north', 'east', 'west' and 'central'

- **Exploratory Data Analysis (EDA)**: 

    Distribution of flight prices: <ins>$40 – 50 is the most common flight prices<ins>

    ![distribution](./pictures/distribution_of_flight_prices_1.png "distribution")

    Average flight price by calendar day: <ins>Flight price is the most expensive on 1st & 6th of the month<ins>
  
    ![distribution](./pictures/calendar_day.png "distribution")

    Average flight price by month: <ins>Flight price is the lowest in April<ins>
    
    ![distribution](./pictures/month.png "distribution")

    Average flight price by booking in advance (days): <ins>Flight price is the highest if one books and travels on the same day<ins>
    
    ![distribution](./pictures/booking_in_advance.png "distribution")

    Flight prices across different durations: <ins>Flight prices positively correlates with durations<ins>
    
    ![distribution](./pictures/durations.png "distribution")

    Flight price by departure session: <ins>Flight price is lowest if departure session is dawn<ins>
    
    ![distribution](./pictures/departure.png "distribution")

    Flight price by arrival session: <ins>Flight price is slightly lower if arrival session is morning or afternoon<ins>
    
    ![distribution](./pictures/arrival.png "distribution")


## Key Features
- Town
- Floor Area (sqm) 
- Lease Commence Year 
- Transaction Year 
- Transaction Month 
- Distance to Mall, Hawker & MRT
- Storey Range



## Modeling - Linear Regression
- Correlation between key factors < ±0.9
- Linear relationship between flight price and different factors .

- Model 1 (Using Group 1)

  ![distribution](./pictures/linreg_1.png "distribution")

  - RMSE: 33.51
  - R<sup>2</sup> Score : 0.6112


- Model 2 (Using Group 1 + Group 2)

  ![distribution](./pictures/linreg_2.png "distribution")

  - RMSE: 33.50
  - R<sup>2</sup> Score : 0.6115

## Exploring Other Models
  | Criteria | Gradient Boosting | Random Forest | Cat Boost | XGB |
  | --- | --- | --- | --- | --- |
  | RMSE | 24.24 | 23.89 | 21.89 | 22.76 |
  | R<sup>2</sup> Score | 0.7966 | 0.8024 | 0.8341 | 0.8206 |


## Recommendations
It is recommended to use CatBoost Regression for this task, as it consistently yields the lowest RMSE and the highest R² score compared to other models. This machine learning technique effectively leverages features from both Group 1 and Group 2, making it particularly well-suited for predicting flight prices.
The model is designed to forecast daily flight prices for competing airlines up until the journey date by incorporating real-time data. Swift Airline can use this information to dynamically adjust its own pricing strategy. 


**Case 1: Flash sales by competitor on similar route**

When the model predicts that a competitor is running a flash sale or offering temporary price reductions on similar routes, particularly during off-peak periods, Swift Airline can adjust its prices in real-time. By matching the competitor’s lower prices, the airline can maintain its market share and avoid being outpriced, ensuring it remains competitive while preserving customer loyalty.

**Case 2: Capitalizing on High Demand**

Conversely, when the model predicts that flight prices are generally high due to increased demand (e.g., during peak travel seasons), Swift Airline can raise its prices in line with competitors’ fares. By doing so, the airline can maximize revenue without risking customer attrition, ensuring that it capitalizes on favourable market conditions.
By continuously updating price predictions based on real-time data, the CatBoost Regression model enables Swift Airline to stay agile and competitive in an ever-changing market landscape. This dynamic approach allows the airline to optimize pricing, increase profitability, and maintain its position in a competitive industry.



## Future Work

The model needs to be trained on a larger dataset to improve its performance. Once sufficient training data is available, the next step is to assess feature importance, which helps identify the most relevant features for the model. This step is crucial for understanding which inputs contribute the most to the predictions. After evaluating feature importance, hyperparameter tuning should be performed to optimize the model's settings and enhance its ability to make accurate predictions. By systematically training the model, analyzing feature relevance, and fine-tuning hyperparameters, the overall performance of the model can be significantly improved.

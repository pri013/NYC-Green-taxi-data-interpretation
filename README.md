# NYC-Green-taxi-data-interpretation using CRISPDM and kNN regression 

## Overview

This project analyzes 2018 NYC Green Taxi trip data to understand and predict passenger tipping behavior. Using a structured CRISP-DM data science workflow, I built a k-Nearest Neighbors (k-NN) regression model to predict tip amounts based on trip characteristics.

The project demonstrates end-to-end data analysis, from cleaning large real-world datasets to feature engineering, visualization, and model evaluation.

## What I Did

Cleaned and processed 1M+ taxi trip records

Filtered to credit card payments only (cash tips not recorded)

Removed outliers and fare inconsistencies

Engineered meaningful features (distance, efficiency, time-based indicators)

Applied log transformations and normalization

Built and tuned a k-NN regression model

Evaluated performance using Mean Squared Error (MSE)

## Key Insights

### Trip & Efficiency Patterns

Tips and fare efficiency are higher on weekdays, especially during working hours

Longer early-morning trips show lower efficiency

### Distance & Demand Trends

Average trip distance varies by time of day

Airport trips follow predictable weekday patterns

### Model Performance

Proper feature scaling is critical for distance-based models

Optimal k balances overfitting and generalization

## Tools & Technologies

Language: R

Libraries: tidyverse, caret, FNN, lubridate

Model: k-Nearest Neighbors Regression

Methods: Data cleaning, feature engineering, EDA, model tuning


<img width="619" height="340" alt="plot1" src="https://github.com/user-attachments/assets/f81c536f-7d69-4c42-bb2d-b325400e9923" />


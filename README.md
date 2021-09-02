# Capstone_Repo

 
**Author**: *Ben Bowman*
  
## Overview
- [Business Problem](#Business-Problem)
- [Data](#Data)
   - [Earthquake Data](./data)
- [Methods](#Methods)
- [EDA Results: Notable Features](#EDA-Results-Notable-Features) 
- [Modeling Results](#Modeling-Results)
- [Conclusions](#Conclusions)
- [For More Information](#For-More-Information)
- [Repository Structure](#Repositroy-Structure)
  

## Business Problem

Sadly, in April 2015, a 7.8 magnitude earthquake struck the Gorkha District of Nepal, killing nearly 9,000 and injuring 22,000. In the aftermath, the Naitonal Planning Commision, along with Katmandu Living Labs and the Central Bureau of Statistics, conducted one of the largest post-disaster datasets ever collected.  Part of the data collected is a survey of buildings that includes building characteristics along with the amount of damage each building incurred.  The probelm at hand is to use those building characteristics to predict whether a building suffered Low Damage, Medium Damage, or Complete Destruction.  
 
## Data

The data comes from drivendata.org but was orginally sourced from the Nepal Earthquake Open Data Portal.  It consists of 260,601 records with 38 features plus the target.  The target is ternary: 1 = 'Low Damage', 2 = 'Medium Damage', and 3 = 'Complete Destruction'.  The target is imbalanced: Low Damage = 9.7%, Medium Damage = 56.9%, and Complete Detruction = 33.5%.  

A data dictionary is included in this repository, but the 38 features can broadly be divided into four categories:  binary columns, categorical columns, integer columns, and geographical columns.

Binary columns:  There are 22 binary (or 'flag') columns that use a 1 to designate that a building has that feature, or else a 0. The binary columns are divided into 'has_superstructure' and 'has_secondary_use' characteristics.

Categorical columns:  There are eight categorical columns, with a total of 38 possibles values across all eight columns.

Integer columns:  There are five integer columns.

Geographical columns:  There are three geographical columns, 'geo_level_1_id', 'geo_level_2_id', and 'geo_level_3_id'. Level 1 is the broadest category, with only 30 unique values, followed by level 2 with 1427, and level 3 with 12567. We can assume that this means they represent descending levels of geographic range. So level 1 could be on the order of a city, level 2 a neighborhood, and level 3 a street. We aren't told what exactly they represent, but we at least surmise that they represent incresingly smaller geographical areas.


 #### Data from drivendata.org
    * Nepal_Earthquake_train_labels.csv
    * Nepal_Earthquake_train_values.csv

   
## Methods

### xxxx


    
## EDA Results Notable Features


### House Value and Price Increase Count

![image](./images/house_value_and_price_increase_count.png)

4/5 selected zipcodes contain houses with higher values than the other zipcodes combined. Zip code 28546 has homes with lower values, but a very high price increase rate of change. This indicates an 'up and coming' zip code, where the homes have consistently garnered value throughout time. 

### Pending Ratio and Days on Market
![image](./images/pending_ratio_and_days_on_market.png)
 
The average days a property is on the market is not a sufficient indicator of consumer demand, because pending properties, or properties that have accepted offers, are still considered 'on the market'. To judge consumer readiness, we selected zipcodes that outpreformed the other zipcodes for increased the number of pending houses while having comparitavely lower days on market increases. 

 
## Modeling Results
We build multiple time series models ranging from a simple naive model to a Facebook Prophet model. The metric we chose was `RMSE` since we want the lowest error between the actual and predicted price of houses in the five recommended zip codes. For two of the zip codes, we used SARIMAX since it not only produced a low RMSE but was better at capturing recent trends in the data and using those trends to make predictions five years into the future. For the other three zip codes, we used a Facebook Prophet model. This model was able to get the lowest `RMSE` while still capturing the recent trends in the data and making future predictions based on this. Here are the top 5 zip codes along with their `RMSE` values:

![image](./images/zipcodes.PNG)  
    
## Conclusions
Using our custom score for determination, we selected five US zip codes for the best real estate investments: 84045 (Saratoga Springs, UT), 98642 (Ridgefield, WA), 28546 (Jacksonville, NC), 80016 (Aurora, CO), and 80516 (Erie, CO).  The current and five-year projected prices and ROI’s are as follows:

![image](https://user-images.githubusercontent.com/82840623/131015478-355f1d18-a6d9-4531-9653-0e51d47bd56f.png)

For the best projected ROI, we suggest Aurora, CO, with a current median home price of just over $300k and a projected 2026 median price of $439k (for an expected ROI of nearly 45%).  For investors looking for a less capital-intensive opportunity, we suggest Jacksonville, NC, where current average home prices are only around $179k, and expected five-year ROI is almost 27%.

    
    
## For More Information
Please review our full analysis in different notebooks [Data Processing Notebook](./01_data_preparation.ipynb), [First Set of Models Notebook](./02_logistic_regression_knn_svm.ipynb), [Random Forest Model Notebook](./03_random_forest_models.ipynb), [XGBoost Notebook](./04_xgboost.ipynb), [Feature Engineering Notebook](./05_feature_engineering.ipynb), [Visualizations Notebook](./06_visualizations.ipynb), and our [Final Notebook](./07_svm_rfc.ipynb) or our [Presentation](./Presentation.pdf).    
    
## Repositroy Structure
```
├── data                                  <- Sourced from an external source
├── images                                <- Images that were used in the presentation and notebooks

    └── Aurora_CO_80016.ipynb                  <- Data Prep Notebook
    └── Erie_CO_80516.ipynb                    <- Erie, CO, 80516 Notebook
    └── Jacksonville_NC_28546.ipynb            <- Jacksonville, NC, 28546 Notebook
    └── Phase_4_functions.py                   <- Phase 4 functions Notebook
    └── Ridgefield_WA_98642.ipynb              <- Ridgefield, WA, 98642 Notebook
    └── Saratoga Springs_UT_84045.ipynb        <- Saratoga Springs, UT, 84045
    └── zip_code_selection_and_one_model.ipynb <- Data Prep Notebook
├── gitignore                             <- python files to ignore 
├── Presentation.pdf                      <- PDF of our project presentation  
├── Data Dictionary.txt                   <- Data Dictionary
└── README.md                             <- The README.md
```
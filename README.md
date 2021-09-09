# Capstone_Repo

 
**Author**: *Ben Bowman*
  
## Overview
- [Business Problem](#Business-Problem)
- [Data](#Data)
   - [Earthquake Data](./Data)
- [Methods](#Methods)
- [EDA Results: Notable Features](#EDA-Results-Notable-Features) 
- [Modeling Results](#Modeling-Results)
- [Conclusions](#Conclusions)
- [For More Information](#For-More-Information)
- [Repository Structure](#Repositroy-Structure)
  

## Business Problem

Sadly, in April 2015, a 7.8 magnitude earthquake struck the Gorkha District of Nepal, killing nearly 9,000 and injuring 22,000. In the aftermath, the National Planning Commission, along with Katmandu Living Labs and the Central Bureau of Statistics, conducted one of the largest post-disaster datasets ever collected.  Part of the data collected is a survey of buildings that includes building characteristics along with the amount of damage each building incurred.  The problem at hand is to use those building characteristics to predict whether a building suffered Low Damage, Medium Damage, or Complete Destruction.  
 
## Data

The data comes from drivendata.org but was originally sourced from the Nepal Earthquake Open Data Portal.  It consists of 260,601 records with 38 features plus the target.  The target is ternary: 1 = 'Low Damage', 2 = 'Medium Damage', and 3 = 'Complete Destruction'.  The target is imbalanced: Low Damage = 9.7%, Medium Damage = 56.9%, and Complete Destruction = 33.5%.  

A data dictionary is included in this repository, but the 38 features can broadly be divided into four categories:  binary columns, categorical columns, integer columns, and geographical columns.

Binary columns:  There are 22 binary (or 'flag') columns that use a 1 to designate that a building has that feature, or else a 0. The binary columns are divided into 'has_superstructure' and 'has_secondary_use' characteristics.

Categorical columns:  There are eight categorical columns, with a total of 38 possibles values across all eight columns.

Integer columns:  There are five integer columns.

Geographical columns:  There are three geographical columns, 'geo_level_1_id', 'geo_level_2_id', and 'geo_level_3_id'. Level 1 is the broadest category, with only 30 unique values, followed by level 2 with 1427, and level 3 with 12567. We can assume that this means they represent descending levels of geographic range. So level 1 could be on the order of a city, level 2 a neighborhood, and level 3 a street. We aren't told what exactly they represent, but we at least surmise that they represent increasingly smaller geographical areas.


 #### [Data from drivendata.org](https://www.drivendata.org/competitions/57/nepal-earthquake/data/)


   
## Methods

I first merge the values and labels dataframes on ‘building_id’ (a unique descriptor for each building), and then determine the target distribution.  I divide the columns into four categories:  eight categorical columns (with 38 unique features across all eight columns), 22 binary (flag) columns, five integer columns, and three geographical columns.  

Categorical columns:  These will be one hot encoded for modeling 

Binary columns:  Use a 1 to designate that a building has that feature, or else a 0. The binary columns are divided into 'has_superstructure' and 'has_secondary_use' characteristics.

Integer columns:  I investigate the distribution of these features and can use log transformation and scaling for modeling.
 
Geographical columns: There are three geographical columns, 'geo_level_1_id', 'geo_level_2_id', and 'geo_level_3_id'. Level 1 is the broadest category, with only 30 unique values, followed by level 2 with 1427, then level 3 with 12567. We can assume that this means they represent descending levels of geographic range. So level 1 could be on the order of a city, level 2 a neighborhood, and level 3 a street. We aren't told what exactly they represent, but we at least surmise that they represent increasingly smaller geographical areas.  I will use Target Encoding on these features for modeling. 

I investigate the correlations between the features and the target and note that there are weak correlations across the board.  In fact the strongest (absolute) correlation is less than .3.

I also construct a baseline Random Forest model to investigate feature importances.  I note that the geographical features are the top three, followed by age of the building.  Some features have minimal importance, and I use various minimum thresholds to investigate dropping some features while modeling.  

I build a dummy model that predicts the most frequent target, which yields a Micro Averaged F1 Score (see below) of .5689.  I then proceed to build and evalute various models, using Logistic Regression, Random Forest, various boosting models, SVM, KNN, stacked models, and a Neural Network.  This is further discussed in the 'Modeling Results' section.


    
## EDA Results & Notable Features


### Target Distribution

![target_distribution](https://user-images.githubusercontent.com/82840623/132359376-bd6ffc6b-fed4-4c69-9f5a-2b9dd1b934a8.png)

The target is encoded as follows: 1 = 'Low Damage', 2 = 'Medium Damage', 3 = 'Complete Destruction'.  There is a target imbalance: 9.7% are 'Low Damage', 56.9% are 'Medium Damage', and 33.5% are 'Complete Destruction'.  

### Age of the Building

![age](https://user-images.githubusercontent.com/82840623/132360170-4cdff715-8395-43f0-bc44-8a3f4c5930c7.png)

The age of the building has an effect on the damage level received.  As the age of the building increases from new to around 30 years, the percentage of buildings that were completely destroyed increases, while the percentage of buildings receiving low damage decreases.  Interestingly, after about 30 years of age, this effect wanes, and the levels of damage are roughly similar for buildings older than that.  
 
 ### Number of Floors

![floors](https://user-images.githubusercontent.com/82840623/132361726-25c5d4e0-ea90-462d-8e10-687ab3829f1f.png)

The damage received increases as the number of floors increases from one to three.  Interestingly, though, as the number of floors increases above three, the level of damage decreases.  We might surmise that this is because buildings taller than three floors are constructed with sturdier materials, I topic discussed under the next graphic.

### Building Superstructure

![superstructure](https://user-images.githubusercontent.com/82840623/132362821-ee2d18ba-c317-4a80-ba82-e3857dafc6d6.png)

This graphic shows the level of complete destruction based on the materials used for the building’s superstructure.  Stone structures fared worst, followed by adobe mud and mud mortared brick.  Timber and bamboo structures were in the middle.  Better performing was cement mortared stone and non-engineered reinforced concrete (RC).  Cement mortared brick performed very well.  But by far the best structure for surviving the earthquake was engineered reinforced concrete.  
 
## Modeling Results

The metric used for evaluating models is the Micro Averaged F1 Score.  An F1 score reflects a blend of the precision and recall of the model, traditionally used on a binary classifier.  Since there are three possible labels, I will use the Micro Averaged F1 Score variant.  
 
![image](https://user-images.githubusercontent.com/82840623/132690917-eef367e7-2cd5-4968-a1f5-ebfedd97be83.png)
 
 
## Conclusions


    
    
## For More Information
Please review my full analysis in different notebooks: [EDA Notebook](./01_Data_Exploration.ipynb), [Random Forest Models Notebook](./02_Random_Forest.ipynb), [PCA Notebook](./03_PCA.ipynb), [Logistic Regression Notebook](./04_LogisticRegression.ipynb), [Boosters Notebook](./05_Boosters.ipynb), [SVM Notebook](./06_SVM.ipynb), [KNN Notebook](./07_KNN.ipynb), [Stacking Notebook](./08_Stacking.ipynb), [Neural Network Notebook](./09_Neural_Network.ipynb), and the [Final Notebook](./) or the [Presentation](./Presentation.pdf).    
    
## Repositroy Structure
```
├── data                                  <- Sourced from drivendata.org
├── images                                <- Images that were used in the presentation and notebooks

└── 01_Data_Exploration.ipynb             <- EDA Notebook
└── 02_Random_Forest.ipynb                <- Random Forest Models
└── 03_PCA.ipynb                          <- Principal Component Analysis
└── 04_LogisticRegression.ipynb           <- Logistic Regression Models
└── 05_Boosters.ipynb                     <- Boosted Models
└── 06_SVM.ipynb                          <- Support Vector Machines Models
└── 07_KNN.ipynb                          <- K-Nearest Neighbors Models
└── 08_Stacking.ipynb                     <- Stacked Model
└── 09_Neural Network.ipynb               <- Neural Network Model
├── gitignore                             <- Python files to ignore 
├── Presentation.pdf                      <- PDF of the project presentation  
├── Data_Dictionary.txt                   <- Data Dictionary
└── README.md                             <- The README.md
```

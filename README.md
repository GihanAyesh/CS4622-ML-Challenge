# 170676P-DrivenData-CS4622

Highest score = **81.82** 
Rank = **1399** 

Github Code Link = [https://github.com/GihanAyesh/170676P-DrivenData-CS4622.git](https://github.com/GihanAyesh/170676P-DrivenData-CS4622.git)

![Submission](/images/sub.jpg)

## Exploratory Data Analysis

The dataset contained 39 features.

### Main findings from EDA

* The majority of the variables are categorical and a small number of numerical, boolean and temporal features exist.
* num_private has zeros for 99% of the rows 
* recorded_by has only one value.
* scheme_name has over 50% of null values

### The following features have null values

* funder 
* installer 
* subvillage 
* public_meeting 
* scheme_management 
* scheme_name
* permit 
 
### The following features have high correlation

* Region and region_code 
* extraction_type, extraction_type_group and extraction_type_class 
* management and management_group 
* payment and payment_type
* water_quality and quality_group 
* quantity and quantity_group 
* source source_type and source_class 
* waterpoint_type and waterpoint_type_group

#### Univariate distribution of population distribution

![population](/images/pop.png)

#### Scatterplot of longitude and latitude

![Longitude](/images/long.png)
![Latitude](/images/lati.png)

## Preprocessing

### Following columns were dropped

* Id - Every row has a unique value
* subvillage, lga, ward, wpt_name - Too many unique values
* extraction_type_group and extraction_type_class - Highly correlated with extraction_type                      
* Num_private - 99% of the rows are zeros
* region- Highly correlated with region_code   
* Recorded_by - Has only one value for every row                                  
* scheme_name - Over 50% of the rows has null
* Payment - Highly correlated with payment_type  
* quality_group- Highly correlated with water_quality    
* quantity_group- Highly correlated with quantity  
* source_type source_class- Highly correlated with source   
* waterpoint_type_group- Highly correlated with waterpoint_type   

### Null values were filled on following columns

* funder, installer, permit - Using value ‘other’ 
* public_meeting - Using value True

### Encodings

* gps_height - Binning
* basin, funder, scheme_management, installer, extraction_type, payment_type, management,  management_group, water_quality, quantity, source, waterpoint_type - One hot encoding
* Status_group - Label encoding

### Other preprocessing steps

* Min max scaler is used before feeding the data to neural network
* Standard scaler is used before feeding to XGBoost
* Longitude and latitude are feature crossed to get a new feature for neural network
* funder, scheme_management, management, installer - labels with low counts were changed to other category
* date_recorded is turned to date-time dtype and the year is filtered out
* Amount_tsh, population - Normalized using standard scaler

## Models used with parameters

### Random Forest

n_estimators=200, max_depth=None, min_samples_split=6, min_samples_leaf=1, max_features='auto', bootstrap=True, warm_start=True

### XGBoost

 base_score=0.5, booster='gbtree', colsample_bytree=0.4, gamma=0.0, importance_type='gain', learning_rate=0.05,max_depth=3, min_child_weight=7, n_estimators=100,n_jobs=1,num_class=3, objective='multi:softmax', random_state=0, reg_lambda=1, scale_pos_weight=1,subsample=1, verbosity=1

### Ada Boost

n_estimators=50, learning_rate=1.0, random_state=None

### Logistic Regression

multi_class='multinomial'

### Neural network

test_size=0.2, learning_rate = 0.001, epochs = 150, batch_size = 4096, validation_split = 0.1

*Hyper parameter tuning is done to Random Forest, XGBoost and Neural Network*

## Feature importance (XGBoost)

![Features](/images/feature.png)
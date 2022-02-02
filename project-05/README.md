--- 

# Project 5: New York's 2019 Volunteer Analysis

--- 

## Executive Summary


### Problem Statement

Going into 2022, the city of New York is trying to identify ways to improve engagement and ensure more volunteers for the upcoming year. 

Utilizing New York's 2019 Volunteers Count Report Boroughs, this project aims to explore the volunteer count compared to area, organization type, interest areas, and boroughs served, to see if there is a relationship between the amount of volunteers and these features

This project will be utilizing the the 2019 Volunteers Count Report Boroughs from [data.world](https://data.world/city-of-ny/yunp-vs8g/workspace/file?filename=2019-volunteers-count-report-boroughs-1.csv).
The type of models that will be developed are Linear Regression and Random Forest and will be evaluated based on the RMSE and accuracy in which the model is able to predict the volunteer count.

### Description of Data

From the ['2019-volunteers-count-report-boroughs-1.csv'](../datasets/2019-volunteers-count-report-boroughs-1.csv), we created several CSV files outs of columns where we utilized .explode() and dummified the features.

- Interest Areas: ['interest_areas_split_total.csv'](../datasets/interest_areas_split_total.csv)
- Organization Types: ['organization_type_split_total.csv'](../datasets/organization_type_split_total.csv)
- Special Populations Served: ['unique_special_pop.csv'](../datasets/unique_special_pop.csv)
- Boroughs Served:['unique_boroughs'](../datasets/unique_boroughs.csv)

Final cleaned dataframe with the dummified features:

- ['df_5'](../datasets/df_5.csv)

Final cleaned dataframe with the dummified and SMOGN features:
- ['df_smogn'](../datasets/df_smogn.csv)

#### Size
- The size of the `2019-volunteers-count-report-boroughs-1.csv` dataset is 544 rows and 23 columns.
- The size of the `df_5.csv` dataset is 540 rows and 85 columns.
- The size of the `df_smogn` dataset is 737 rows and 85 columns.

#### Source
Provided from [data.world](https://data.world/city-of-ny/yunp-vs8g/workspace/file?filename=2019-volunteers-count-report-boroughs-1.csv) and [NYC OpenData](https://data.cityofnewyork.us/Social-Services/2019-Volunteers-Count-Report-Neighborhoods/72r6-mtgs).

#### Target
Target is a regression analysis predicting volunteer count.

#### Data Dictionary
- Data dictionary can be found on [data.world](https://data.world/city-of-ny/yunp-vs8g/workspace/data-dictionary).
- Datasets included in data dictionary are datasets from each final model.
- One-hot encoding was used on columns `organization_type`, `interest_areas` and `boroughs_served`. This created numerous new features that are not included in the data dictionary, but are derived from the features listed below.

|Feature|Type|Dataset|Description|
|---|---|---|---|
|total_volunteers|integer|2019-volunteers-count-report-boroughs-1|Total count of volunteers (teen, adult, and older adults)|
|organization_type|object|2019-volunteers-count-report-boroughs-1|Type of organizations|
|interest_areas|object|2019-volunteers-count-report-boroughs-1|Type of interest area(s)|
|boroughs_served|object|2019-volunteers-count-report-boroughs-1|Areas where the organization serves|

#### Model Performance on Training/Test Data
|Model|Train Score|Test Score|
|---|---|---|
|Baseline: Linear Regression|0.1813|-1.079|
|Linear Regression: PCA|0.0836|0.019|
|Linear Regression: PCA Gridsearch|0.0497|0.0316|
|Random Forest: PCA Gridsearch|0.774|-1.466|
|Random Forest: SMOGN|0.713|0.529|
|Random Forest: SMOGN & Gridsearch|0.633|0.485|

### Conclusion
Overall, our models were overfit. With our initial problem statement, we wanted to analyze the different subsets of volunteers (teens, adult, older adults), but found that our dataset had a lot of missing values that did not make this problem statement appropriate. We then decided to focus on interest areas and organization types. Because the input for these sections were based on what the charity entered into the survey, many values were duplicated and/or had many rows that were stating the whole mission statement/sentence for what their interest area or organization type is (example: "non profit" vs. "Non-profit" vs. "not for profit"). This came as a challenge and we decided to remove interet areas that had less than 10 rows. 

With a bunch of exploded and dummified columns, we decided to run PCA to help with dimensionality reduction and help identify important relationships in our data.

We ran a baseline linear regression model, but because the dataset did not adhere to the LINE assumptions, running a linear regression model was not the best model and we decided to run a random forest regressor.

Lastly, we decided to inflate our dataset and oversample the total population to get more data. In conclusion, with the random forest model we ended up with a train score: 0.713 and test score: 0.529 and a train RMSE: 2670.93 and test RMSE: 3645.51. When using a gridsearch for the random forest we got a train score: 0.633 and test score: 0.485 and a train RMSE: 3018.84 and test RMSE: 3811.52. Comparing the two, the gridsearch had less overfitting, but had a higher RMSE than the random forest without gridsearch.

### Next Steps
Next Steps:
- Use the `special_populations_served` column in the model by cleaning, exploding and dummify the column
- Further clean the `organization_type` and `interest_areas` column by combining rows that had a value of less than 10 rows if the rows were the same type of organization or interest area. We decided to drop all organization types that had less than 10 rows, but for example, some types could have been combined to create a "food resource" type.
- Bring in more data such as Census data to further investigate relationships of charities in New York
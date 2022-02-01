--- 

# Project 2: Ames Housing Data Analysis & Price Prediction

--- 

## Executive Summary

### Problem Statement

Utilizing the Ames Housing Data and building regression models (linear, LASSO, ridge), how can we predict the pricing on houses in Ames, Iowa?

"While most people tend to fix up their own house to continue to live in it, there’s a new generation of relatively young entrepreneurs in their 20s and 30s who make a living as house flippers. They buy a house at a low price and live in it while fixing it up– themselves and/or with the help of professionals. Then, after a few months, they “flip” it for more money than they paid for it and invested in it, making a profit ([*source*](https://mmlending.com/the-history-of-house-flipping/))."

There is a workshop presented by Magnolia Homes for attendees interested in buying and reselling homes. The company will share ideas on important features to focus on when fixing up a house.

The metric for accurate price prediction will be measured and evaluated by the root mean squared error of the regression.

### Description of Data
From the [`train.csv`](./datasets/train.csv), I created [`train_final.csv`](./datasets/train_final.csv), [`train_final2.csv`](./datasets/train_final2.csv), [`train_final3.csv`](./datasets/train_final3.csv). These 3 datasets have the 3 different models that I generated on Sales Price.

- [`saleprice.csv`](./datasets/saleprice.csv) which has the `Id` and `SalesPrice`.

- [`submission_1.csv`](./datasets/submission_1.csv)
- [`submission_2.csv`](./datasets/submission_2.csv)
- [`submission_3.csv`](./datasets/submission_3.csv)


#### Size
The size of the `train_final.csv` dataset is 1883 rows and 35 columns.
The size of the `train_final2.csv` dataset is 1883 rows and 31 columns.
The size of the `train_final3.csv` dataset is 1883 rows and 41 columns.

#### Source
Provided from the project-02-main Dataset:
- [`train.csv`](./datasets/train.csv): Ames Housing Training Dataset
- [`test.csv`](./datasets/test.csv): Ames Housing Testing Dataset

#### Target
Target is a regression analysis predicting sales price on housing.

#### Data Dictionary
- Full data dictionary can be found on ([Kaggle](https://www.kaggle.com/c/dsirfx817/data)).
- Datasets included in data dictionary are datasets from each final model.
- One-hot encoding was used on all features that are object type. This created numerous new features that are not included in the data dictionary, but are derived from the features listed below.


|Feature|Type|Dataset|Description|
|---|---|---|---|
|MS SubClass|integer|train_final, train_final2, train_final3|The bulding class|
|Lot Area|integer|train_final, train_final2, train_final3|Lot size in square feet|
|Overall Qual|integer|train_final, train_final2, train_final3|Overall material and finish quality|
|Overall Cond|integer|train_final, train_final2, train_final3|Overall condition rating|
|Year Built|integer|train_final, train_final2, train_final3|Original construction date|
|Year Remod/Add|integer|train_final, train_final2, train_final3|Remodel date (same as construction date if no remodeling or additions)|
|Total Bsmt SF|integer|train_final, train_final2, train_final3|Total square feet of basement area|
|Gr Liv Area|integer|train_final, train_final2, train_final3|Above grade (ground) living area in square feet|
|Bedroom AbvGr|integer|train_final, train_final2, train_final3|Bedroom above grade in square feet|
|Kitchen AbsGr|integer|train_final, train_final2, train_final3|Kitchen above grade in square feet|
|TotRms AbvGrd|integer|train_final, train_final2, train_final3|Total rooms above grade (not including bathrooms)|
|Enclosed Porch|integer|train_final, train_final2, train_final3|Enclosed porch area in square feet|
|Screen Porch|integer|train_final, train_final2, train_final3|Screen porch area in square feet|
|Garage Area|integer|train_final, train_final2, train_final3|Size of garage in square feet|
|Mas Vnr Area|integer|train_final2, train_final3|Masonry veneer type|
|Neighborhood|object|train_final, train_final2, train_final3|Physical locations within Ames city limits|
|Exter Qual|object|train_final3|Exterior material quality|
|Bsmt Exposure|object|train_final3|Walkout or garden level basement walls|
|Kitchen Qual|object|train_final3|Kitchen quality|

#### Model Performance on Training/Test Data

In total, I fit 7 different models utilizing 3 different sets of features (train_final, train_final2, train_final3). For each set of features, I did a linear regression model, lasso regression model, and generated a ridge regression for the first set of features (train_final)

|Model|Type of Regression|RMSE Train Score|RMSE Test Score|
|---|---|---|---|
|Model 1|Linear Regression|30829.70|31525.39|
|Model 1|Lasso Regression|29353.42|24989.16|
|Model 1|Ridge Regression|29237.84|25083.19|
|Model 2|Linear Regression|28293.83|26571.27|
|Model 2|Lasso Regression|28276.48|23978.25|
|Model 3|Linear Regression|24426.56|23206.78|
|Model 3|Lasso Regression|24146.74|22099.89|

### Conclusion/Recommendations

#### Conclusion
- In conclusion, using the LASSO regression helped eliminate features with low or 0 coefficients.
- The root mean squared error was also typically lower when comparing the LASSO and linear regression models. 
- When comparing the residuals from the LASSO regression and linear regression, it seemed like the linear regression model was always closer to 0 while the LASSO models were more scattered.
- As I went from the baseline model to model 1, 2, and 3, and added different features the RMSE decreased.
- Because my RMSE was always higher when submitted into Kaggle, insisting that my model may still be overfit.

#### Recommendations
Overall, based on these models, I have recommendations on the 5 best features that will impact values of sales price and 5 features that will lower the value of a home.

Ranking from highest to lowest is:
Ground living area, year built, total basement in square feet, overall material and finish quality, and the neighborhoods Stonebrook, Northridge Heights and Northridge would be great neighborhoods with higher selling price.

Based on the data, it would be beneficial for flippers to pay attention to these specific neighborhoods and to the overall size of the living room and basement when picking the property. It is also important to ensure that the overall material and finish quality is very good to excellent when renovating the home. It would also be important to pay attention to the year built, but I think because you are flipping a home, this may not be as significant if the renovations modernizes some of the outdated aspects of the home.

Ranking from highest to lowest again where highest has a more negative coefficient, the first is kitchen quality that is average or good, exterior quality that is average or good, the MS subclass, and neighborhoods Northwest Ames, North Ames, and Old Town.
In terms of flipping a house, in renovations, I think it is important to have a kitchen and exterior quality that is in excellent condition.

In terms of flipping a house, in renovations, it is important to have a kitchen and exterior quality that is in excellent condition.

### Next Steps
To further investigate this problem statement and to go into more detail, I would utilize all the categorical data, use one-hot encoding, then run a lasso regression to eliminate the features with no significant coefficient. I also would run other regression models such as ridge to help compare my models from one another. I utilized ridge regression on 1 model and did not realize until reviewing my notebook that the ridge model did better than the LASSO model that was submitted to Kaggle.

I also would utilize more helper functions to help organize and eliminate repetition in my code especially when repeating the input of colums from the train dataset to the testing dataset.

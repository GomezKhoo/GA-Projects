

General Assembly Project 2: Ames House Price Prediction

Author: Khoo Qi Xiang (DSI31)


This project comprises 2 notebooks:

Part 1 - Data Cleaning, EDA, Feature engineering

Part 2 - Modelling, Prediction and Conclusion.

## Introduction


Property valuators does not know the true market value of their homes. This results in a unfair payment of property tax based on valuation of property as different valuators would valuate a property different.

In this project, we would be making three supervised machine learning models; Linear Regression model, Ridge Regression model and Lasso regression model, using train data to test the model against the test data to predict the property sale price. 

## Problem Statement
- The main objective of this model is to set a predicted valuation/price of a property in line with the market perceived value of the property, allowing valuators to set a fair price for the property and hence fair property taxes for everyone who would be paying property tax.
 
## Dataset 
- train.csv -- this data contains all of the training data for your model. The target variable (SalePrice) is removed from the test set!
- test.csv -- this data contains the test data for your model. You will feed this data into your regression model to make predictions.

http://jse.amstat.org/v19n3/decock/DataDocumentation.txt

## Data Cleaning and Featuring Engineering
The train dataset has all of the columns that we will need to generate and refine your models. The test dataset has all of those columns except for the target that you are trying to predict in your Regression model.
Generate your regression model using the training data. We expect that within this process, you'll be making use of:
- train-test split
- cross-validation 
- strong exploratory data analysis to question correlation and relationship across predictive variables.

After Data cleaning and featuring engineering, we managed to cut down to around 38 features that were used to input into the regression model.

## Summary of the three models:

- Linear Regression Model: Test set RMSE of 25,475 thousand and R-square scoreof 0.900.
- Ridge Regression Model: Test set RMSE of 25,506 thousand and R-square score of 0.900.
- Lasso Regression Model: Test set RMSE of 25,095 thousand and R-square score of 0.903.

Lasso Regression model performing the best with the highest R2 score and lowest RSME. All the other regression models are performing with a decent R-squared and stable RMSE values. The most ideal result would be an RMSE value of zero and R-squared value of 1, but that's almost impossible in real economic datasets.

Properties of prices ranging from USD 100,000 to USD 350,000 are well predicted with small deviations from actual sale price. Beyond USD 350,0000, the prediction deviates further. We can observed that prediction begin to diverge from the actual sale price and under-estimation occurs more frequently than over-estimation. This is most likley caused due to the insufficient amount of data available for prices beyond USD 350,000 which causes the more expensive properties to be not well predicted.

## Limitation

There were a few limitation of the lasso model and dataset that we worked:
- If the number of predictors are greater than the number of observations, Lasso will pick at most predictors as non-zero, even if all predictors are relevant.
- Lasso regression will select one of them randomly when there are two or more highly collinear variables. This will cause wrong interpretation of certain datas.
- As some features have too little data but could be play as an important feature, using lasso will just completely eliminate it.

## Recommendation

Through our findings, we recommend:
- Having an excellent kitchen quality will increase in sale price so maybe realtors can suggest to prospective sellers to do facelift works to kitchen before putting up on the market.
- Same goes for exterior quality, it should be well maintain or good condition and those can increase the sale price.
- Fireplaces play a suprising factor for this model and its show that a good fireplace is wanted by the resident and this could be due to winter season with good fireplace, the house will be protected from the cold.

## Suggestion for further analysis:
- Using hyperparameter to obtain a model with optimal performance.
- Filter features that were greatly reduced by ridge regression and also eliminated by lasso regression to improve model.
- Better feature engineer some of the features.
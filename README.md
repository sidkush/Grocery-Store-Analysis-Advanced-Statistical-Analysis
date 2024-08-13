# Grocery Store Analysis

## Business Problem Statement
The purpose of this project is to build an efficient sales modeling system for a retail organization using prior sales data and additional datasets provided. The goal is to utilize statistical techniques to understand the relation between oil prices, unit sales, transactions, store type, and store locale.

## Methodology
The analysis was conducted on a Grocery Stores dataset with n=100,000 random daily sampled values for six variables of interest:
- Date
- Id
- Type (Store Type: A, B, C, D, E)
- Locale (National, Regional, Local)
- Unit Sales
- Dcoilwtico (Daily oil prices)

The methodology involved the following steps:
1. Preliminary investigation of statistical measures of dataset features
2. Initial visualizations and assumptions regarding variable behavior
3. Determining the distribution of each random variable
4. Central Limit Theorem exploration: Investigating transactions
5. Constructing a confidence interval for transactions from random samples
6. Hypothesis testing using the same random transactions sample
7. Comparing different datasets: Type and Locale with Transactions
8. Model implementation and results

## Key Findings from EDA
- The standard deviation for transactions is very high, suggesting a huge variance in the dataset.
- The mean values are very low compared to the maximum value, indicating right-tail skewness in the dataset.
- Unit prices also seem to have right-skewed data.
- Transactions and Type show a negative but not significant correlation.
- Major transactions were related to the National Locale compared to other attributes.
- D type stores contribute more towards the total revenue of the Grocery Chain.
- Oil prices have high variance, with increased volatility in later years.
- Transactions and Dcoilwtico are not normally distributed, even after applying the Yeo-Johnson transformation.
- Unit Sales data does not follow a normal distribution, even after transformation.

## Model Implementation and Results
The analysis used various regression models to predict the Transactions variable:

1. Ordinary Least Squares (OLS) Regression:
   - The model had a good F-statistic value and p-value of 0 for all features but a low R² value (0.315), indicating that the model could not explain the variance in the Transactions variable.
   - Residuals showed patterns and deviated from the line in the QQ plot, suggesting non-normality in the residuals.

2. Polynomial Regression:
   - Using GridSearchCV, the best hyperparameters were obtained at n=3 with an R² value of 0.59.
   - Residuals appeared randomly scattered, and the QQ plot was closer to the straight line, suggesting a normal distribution of residuals.
   - Polynomial Regression was able to understand and predict the model more accurately than OLS and Decision Tree Regressor.

3. Decision Tree (DT) Regressor:
   - Using GridSearchCV, the best hyperparameters were obtained at max_depth=9 and min_samples_split=5 with an R² value of 0.69.
   - Although DT Regressor could explain more variance in the target variable compared to Polynomial Regression, the residual plot showed more scatter in Polynomial Regression, and the QQ plot was more stable.

4. One Hot Encoding (OHE):
   - OHE increased the total number of features and improved the OLS model's R² value to 0.545 and the F-statistic value.
   - However, some features became insignificant for the model with high p-values after introducing OHE.
   - OHE improved the learning of the Polynomial model, increasing the R² value to 0.60 and resulting in a more scattered residual plot.
   - Increasing dimensions did not affect DT Regressor, but Polynomial Regression outperformed DT.

## Conclusion
The analysis revealed that data preprocessing, including outlier treatment using the Yeo-Johnson method and handling qualitative variables using OHE, was necessary before applying the models. The investigation found that Transactions had a nonlinear relationship with its predictors, leading to better results with Polynomial Regression compared to OLS and Decision Tree Regressor.

Although DT Regressor could explain more variance in the target variable, the residual plot and QQ plot suggested that Polynomial Regression learned better from the predictors. The spread in the residual plot of DT Regressor indicated that Polynomial Regression outperformed it.

In conclusion, Polynomial Regression with hyperparameter optimization and OHE proved to be the most effective model for understanding and predicting the Transactions variable based on the given dataset and predictors.

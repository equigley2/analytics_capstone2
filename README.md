<h2>Data: Airline flight data from the Bureau of Transportation

>Example below shows flights from Denver to New York City

<h2> Goal: Use linear regression to predict airline delays in minutes based on origin and destination
<h2>Exploratory Data Analysis
* Violin plots - black box show the IQR where 50% of the data resides
* B6 and DL have a small amount of large numbers in the tails. Their mean is likely higher than the others.
* Carrier will be a good predictor going forward
* Day of week will not be as strong of a predictor

 	![](./carrier_violinDtNY.png)
  ![](./day_of_week_violinDtNY.png)
<h2>Feature Engineering
* Selected features to start with
* Filled columns with the mean, the rest with 0s
* Created dummy variables and converted all columns to binary
* Set predicted values as departure delay in minutes
* Selected features as time of day, day of week, month, delay type, and airline carrier

  ```python
  input_city_origin = str(input("What city are you leaving from?"))
  input_city_dest = str(input("What city are you going to?"))"
  ```

* Standardize and transform X values - since I have different units of measurement in my features I need to convert all columns to a mean of 0 and standard deviation of 1


<h2>Modeling
* Split into training and testing data
* Fit statsmodels OLS regression
* Adjusted R squared is strong
* Airlines have the largest coefficients
* Day of week is not looking very significant because of the higher p-value
* Consistent with our EDA

  ![](./ols_summaryDtNY.png)
* Ran my sklearn linear regression taking into account the train and test sets of data
* Fit linear regression on X and y training data
* After my model is fit, predict y values using X test. Returns an array of predicted values


<h2>Results

How did the model do? Let's check our R-Squared value.


  ![](./test_scoreDtNY2.png)

Average predicted delay flying from Denver to NYC.

  ![](./predicted_meanDtNY2.png)


Q-Q Plot
* Values above and below the red line indicate these points are more extreme than we would expect with a normal distribution


  ![](./qq_pltDtNY.png)


Variance Inflation Factors
* To better understand the Q-Q plot I looked at the VIFs
* Measures how much variance increases if your features are correlated
* All VIFs are < 10. If they were over 10, this would signal high multicollinearity


<h2>Future Work
>* Remedy Q-Q plot
* Remove DEP_TIME_BLOCK and check impact
* Fix spacing on plots
* Complete Lasso and Ridge regression to compare models

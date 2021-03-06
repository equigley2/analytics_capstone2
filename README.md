<h2>Data: Airline flight data from the Bureau of Transportation</h2>

4.5 million rows of US flight data. 
Examples below show flights from Denver to New York City.

<h2> Goal:</h2>

Use linear regression to predict airline delays in minutes based on origin and destination</h2>
  
<h2>Exploratory Data Analysis</h2>
  
* Violin plots show the distribution of data
* Black box shows the IQR where 50% of the data resides
* JetBlue and Delta have a small amount of large numbers in the tails. Their mean is likely higher than the others.
* Carrier will be a good predictor going forward
* Day of week will not be as strong of a predictor

<img src='images/carrier_violinDtNY.png'>
  
<img src = 'images/day_of_week_violinDtNY.png'>
  
<h2>Feature Engineering</h2>
  
* Selected features to start with narrowing down to about 30 from approx. 50 rows
* Filled select columns with the mean, the rest with 0s
* Created dummy variables and converted all columns to binary
* Set predicted values as departure delay in minutes
* Selected features as time of day, day of week, month, delay type, and airline carrier

  ```python
  input_city_origin = str(input("What city are you leaving from?"))
  input_city_dest = str(input("What city are you going to?"))"
  ```

* Standardize and transform X values - since I have different units of measurement in my features I need to convert all columns to a mean of 0 and standard deviation of 1


<h2>Modeling</h2>
  
* Split into training and testing data
* Fit statsmodels OLS regression
* Adjusted R squared is strong
* Airlines have the largest coefficients
* Day of week is not looking very significant because of the higher p-value
* Consistent with our EDA

<img src = 'images/ols_summaryDtNY.png'>

* Ran my SKlearn linear regression taking into account the train and test sets of data
* Fit linear regression on X and y training data
* After my model is fit, predict y values using X test.


<h2>Results</h2>

How did the model do? Let's check our R-Squared value.

<img src = 'images/test_scoreDtNY2.png'>

Average predicted delay flying from Denver to NYC.

<img src = 'images/predicted_meanDtNY2.png'>


Q-Q Plot

* Values above and below the red line indicate these points are more extreme than we would expect with a normal distribution


<img src = 'images/qq_pltDtNY.png'>


Variance Inflation Factors

* To better understand the Q-Q plot I looked at the VIFs
* Measures how much variance increases if your features are correlated
* All VIFs are < 10. If they were over 10, this would signal high multicollinearity

<img src = 'images/vifsDtNY2.png'>

<h2>Future Work</h2>
  
* Remedy Q-Q plot
* Remove DEP_TIME_BLOCK and check impact
* Fix spacing on plots
* Complete Lasso and Ridge regression to compare models

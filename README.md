# Covid-19-Cases-Time-Series-Forecasting
**For This Project I Performed time-series forecasting on NY State’s Covid-19 data during the start of the second wave (December 2020).**

I experiment with:
- Auto-Regressive models, 
- Weighted exponential smoothing, 
- manually & Autotuned ARIMA & SARIMA models 
- SARIMAX models (Seasonal ARIMA with supporting exogenous data)
  - The SARIMAX model training process includes hypothesis testing of the exogenous data’s fitment to the covid case data

The End Goal is to develop a model for a 1 month out of sample prediction (1-month forecast) of covid-19 cases for the state with an uper and lower bound defining best and worst case.

**Supporting data used as exogenous for SARIMAX Model:**

Oxfords covid-19 data hub tracks policy measures across 19 indicators. I used the database to pull a variety of Policy related features and examine some of the response indicies created by Oxford (indices are simple averages of the individual component indicators).
- General info: [https://github.com/OxCGRT/covid-policy-tracker#subnational-data](https://github.com/OxCGRT/covid-policy-tracker#subnational-data)
- Indicies: [https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md](https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md)

For example:

<img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/An%20Example%20of%20the%20Oxford%20Database%20Indicators.png" width="500" height="300">

The Project Workflow was as follows:

1. ARIMA
- Auto
- Manual
Results were not good enough. 

2. SARIMA
- Auto
  - Results were good but due to the use of the automatic function, freedom in tuning and adressing caveats was missing.
- Manual 
  - mse 1132324.045
  - rmse 1064.107
  - mape 0.109
  
  <img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/Best%202-Week%20Prediction%20(Manually%20Tuned%20SARIMA).png" width="500" height="300">
  
3. SARIMAX
- Auto
- Started by selecting the top 5 indices most Correlated to covid cases before training my SARIMAX model on them:
  - ConfirmedDeaths
  - 3_Cancel public events
  - C4_Restrictions on gatherings
  - H2_Testing policy
  - H6_Facial Coverings
- Training & Validation
  - mse 2103829.276
  - rmse 1450.458
  - mape 0.112
  
  <img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/SARIMAX%20UnSig.png" width="500" height="300">
  
- Training yields that the only Statistically Significant indices W/ large coefficients (Influence of SARIMAX model) are
  - C4_Restrictions on gatherings
  - H2_Testing policy
-  Model trained with only statistically significant indices
  - mse 2142885.617
  - rmse 1463.860
  - mape 0.113

  <img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/SARIMAX%20Top%205.png" width="500" height="300">

 - Despite all this work on trying to build a SARIMAX model and finding the perfect exogenous data set to support its predictions, the manually tuned SARIMA Model previously built (2) outperforms all SARIMAX models. for that reason, I will use that model to do my one month out prediction.

4. Apply wining SARIMA model for 1-month prediction.
<img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/1%20Month%20out%20prediction%20using%20Best%20Model.png" width="500" height="300">
Forecasting for one month out is as expected a very difficult task as 1 month is a long time however it is reassuring that the forecast's lower bound is very close to actual cases.

A reminder of the 2-week forecast's outcome:

<img src="https://github.com/kamalmukhalalaty/Covid-19-Cases-Time-Series-Forecasting/blob/main/Images/Best%202-Week%20Prediction%20(Manually%20Tuned%20SARIMA).png" width="500" height="300">


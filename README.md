# Covid-19-Cases-Time-Series-Forecasting
**For This Project I Performed time-series forecasting on NY State’s Covid-19 data during the start of the second wave (December 2020).**

I experiment with:
- Auto-Regressive models, 
- Weighted exponential smoothing, 
- manually & Autotuned ARIMA & SARIMA models 
- SARIMAX models (Seasonal ARIMA with supporting exogenous data)
  - The SARIMAX model training process includes hypothesis testing of the exogenous data’s fitment to the covid case data

The End Goal is to develop a model for a 1 month out of sample prediction (1-month forecast) of covid-19 cases for the state with an upper and lower bound defining best and worst case.

**Supporting data used as exogenous for SARIMAX Model:**

Oxfords covid-19 data hub tracks policy measures across 19 indicators. I used the database to pull a variety of Policy related features and examine some of the response indices created by Oxford (indices are simple averages of the individual component indicators).
- General info: [https://github.com/OxCGRT/covid-policy-tracker#subnational-data](https://github.com/OxCGRT/covid-policy-tracker#subnational-data)
- Indices: [https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md](https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md)

For example:

<img width="899" alt="An Example of the Oxford Database Indicators" src="https://user-images.githubusercontent.com/72153772/116601504-94fe9480-a8f8-11eb-8563-524bcb1a1e63.png">

The Project Workflow was as follows:

1. ARIMA
- Auto
- Manual
Results were not good enough. 

2. SARIMA
- Auto
  - Results were good but due to the use of the automatic function, freedom in tuning and addressing caveats was missing.
- Manual 
  - mse 1132324.045
  - rmse 1064.107
  - mape 0.109
  
  <img width="923" alt="Best 2-Week Prediction (Manually Tuned SARIMA)" src="https://user-images.githubusercontent.com/72153772/116601547-a21b8380-a8f8-11eb-94db-1f3eaa2d5a6a.png">
  
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
  
  <img width="907" alt="SARIMAX UnSig" src="https://user-images.githubusercontent.com/72153772/116601615-b0699f80-a8f8-11eb-9a27-194b00b8e1a0.png">  

- Training yields that the only Statistically Significant indices W/ large coefficients (Influence of SARIMAX model) are
  - C4_Restrictions on gatherings
  - H2_Testing policy
-  Model trained with only statistically significant indices
  - mse 2142885.617
  - rmse 1463.860
  - mape 0.113

  <img width="910" alt="SARIMAX Top 5" src="https://user-images.githubusercontent.com/72153772/116601739-d000c800-a8f8-11eb-8798-25651c53afed.png">

 - Despite all this work on trying to build a SARIMAX model and finding the perfect exogenous data set to support its predictions, the manually tuned SARIMA Model previously built (2) outperforms all SARIMAX models. For that reason, I will use that model to do my one month out prediction.

4. Apply winning SARIMA model for 1-month prediction.

<img width="909" alt="1 Month out prediction using Best Model" src="https://user-images.githubusercontent.com/72153772/116601894-ff173980-a8f8-11eb-9191-1a9e16d2dba7.png">

Forecasting for one month out is as expected a very difficult task as 1 month is a long time however it is reassuring that the forecast's lower bound is very close to actual cases.

A reminder of the 2-week forecast's outcome:

<img width="923" alt="Best 2-Week Prediction (Manually Tuned SARIMA)" src="https://user-images.githubusercontent.com/72153772/116601547-a21b8380-a8f8-11eb-94db-1f3eaa2d5a6a.png">

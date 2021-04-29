# Covid-19-Cases-Time-Series-Forcasting

**For This Project I Performed time-series forecasting on NY State’s Covid-19 data during the start of the second wave (December 2020).**

I experiemnt with:
- Auto Regressive models, 
- Weighted exponential smoothing, 
- manually & Auto tuned ARIMA & SARIMA models 
- SARIMAX models (Seasonal ARIMA with supporting exogenous data)
  - The SARIMAX model training process includes hypothesis testing of the exogenous data’s fitment to the covid case data

The End Goal is to develop a model for a 1 month out of sample prediction (1 month forcast) of covid-19 cases for the state with an uper and lower bound defining best and worst case.

**Supporting data used as exogenous for SARIMAX Model:**

Oxfords covid-19 data hub tracks policy measures across 19 indicators. I used the database to pull a variety of Policy related features and examine some of the response indicies created by Oxford (indices are simple averages of the individual component indicators).
General info: [https://github.com/OxCGRT/covid-policy-tracker#subnational-data](https://github.com/OxCGRT/covid-policy-tracker#subnational-data)
Indicies: [https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md](https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md)

The Project Workflow was as follows:

1. ARIMA
- Auto
- Manual
Results were not good enough. 

2. SARIMA
- Auto
  - Results were good but due to the use of the automatic function freedom in tuning and adressing caveats was missing
- Manual 
  - mse 1132324.045
  - rmse 1064.107
  - mape 0.109
 
3. SARIMAX A
- Auto
- Started by selecting the Top 5 indicies most Correlated to covid cases before training my SARIMAX model on them:
  - ConfirmedDeaths
  - 3_Cancel public events
  - C4_Restrictions on gatherings
  - H2_Testing policy
  - H6_Facial Coverings
- Training & Validation
  - mse 2103829.276
  - rmse 1450.458
  - mape 0.112
- Training yeilds that the only Statistically significant indicies W/ large coefficients (Influence of SARIMAX model) are
  - C4_Restrictions on gatherings
  - H2_Testing policy
-  Model trained with only Statsically significant 
    - mse 2142885.617
    - rmse 1463.860
    - mape 0.113
 - Despite all this work on trying to build a SARIMAX model and finding the perfect exogenous data set to support it's predictions, the mannually tuned SARIMA Model previously built outperforms all SARIMAX models. for that reason I will use that model to do my one month out prediction.

4. Apply wining SARIMA model for 1-month prediction.


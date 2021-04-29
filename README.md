# Covid-19-Cases-Time-Series-Forcasting

For This Project I Performed time-series forecasting on NY State’s Covid-19 data during the start of the second wave (December 2020). 

I experiemnt with Auto Regressive models, Weighted exponential smoothing, 

manually tuned ARIMA and SARIMA models 

Create a SARIMAX model (Seasonal ARIMA with exogenous data) models. 

This SARIMAX model includes hypothesis testing of the exogenous data’s correlations.

ADD MORE


Supporting data used as exogenous for SARIMAX Model:

Oxfords covid-19 data hub was used to pull a variety of 
https://github.com/OxCGRT/covid-policy-tracker#subnational-data

Started by selecting the Top 5 most Correlated - (To be discussed in nect section):

ConfirmedDeaths
3_Cancel public events
C4_Restrictions on gatherings
H2_Testing policy
H6_Facial Coverings

Statistically significant W/ large positive coefficients in the sarimax
C4_Restrictions on gatherings
H2_Testing policy


Same Model with removing statistically insignificant exogeneous variables
The goal here is to eliminate the noise coming from the spurrously correlated exogeneous data


Looking at the indices instead.
The Oxford Covid-19 Government Response Tracker (GitHub repo, university website) tracks individual policy measures across 19 indicators, in part 4 I handpicked a couple to analyse for correlation with my case data.

The Oxford Covid-19 Government Response Tracker also calculates several indices to give an overall impression of government activity, and this is how these indices are calculated.

All of our indices are simple averages of the individual component indicators. This is described in equation 1 below where k is the number of component indicators in an index and Ij is the sub-index score for an individual indicator.

https://github.com/OxCGRT/covid-policy-tracker/blob/master/documentation/index_methodology.md


Despite all this work on trying to build a SARIMAX model and finding the perfect exogenous data set to support it's predictions, the mannually tuned SARIMA Model previously built outperforms all SARIMAX models. for that reason I will use that model to do my one month out prediction


SARIMA Manually tuned
mse is 0.8083716716343051
rmse is 0.8990949180338553
mape is 0.03725802334935286

SARIMAX W/ Exogenous top 5 most highly correlated Variables from Policy Tracker (3_Cancel public events, C4_Restrictions on gatherings, H2_Testing policy, H6_Facial Coverings)
mse is 2103829.2763673062
rmse is 1450.4582987343367
mape is 0.1123068311642705

SARIMAX W/ Stat. Sig. Exogenous Variables (Restrictions on gatherings and Testing Policy) from top 5
mse is 2142885.617228333
rmse is 1463.8598352398133
mape is 0.11301532218357295

SARIMAX W/ Stat. Sig. Exogenous Variables from Stringency Index, rmse=1463

mse is 2140597.397295473
rmse is 1463.0780557767494
mape is 0.11332226861611824

# Natural-Disaster-Impact-on-the-Economy

Natural disasters’ effects can threaten the firmness of the economy but are often underestimated. Due to the underestimation of this threat, current economic models in Nigeria don’t often incorporate its impact on key economic indicators, thereby hindering the development of effective strategies to mitigate its effect on the economy. Using the time series model (SARIMA and PROPHET), this research aims to understand natural disasters’ impact (floods) on Nigeria’s economy (crude oil) for early detection of economic recession.


# Data Collection

The dataset was collected from two agencies in Nigeria, NiMet and the Ministry of Finance. This data collected from NiMet, which spans from 2010 – 2023. The dataset focusses on southwest, Nigeria. The southwest has a history of flood disasters.
The crude oil data collected is from the Ministry of Finance include GDP etc. The oil and gas sector were the section of the GDP that was used. This is because crude oil is a major driver of the Nigerian economy. The data also spans from 2010 to 2023.

<img width="899" height="584" alt="image" src="https://github.com/user-attachments/assets/c4be0c6d-c0fa-4aef-949b-0e21d8d6d4e8" />

US crude oil price from 2000 – 2023. This data is recorded monthly, and the price is in dollars.


<img width="613" height="595" alt="image" src="https://github.com/user-attachments/assets/13235b44-08cb-40a1-9335-7a3351a4b3f0" />

Nigeria CrudeOil Price from 2010 – 2023. This data is recorded quarterly, and the price is in Naira.

# Data Exploration

Seasonal Decomposition
This is one of the methods in which seasonality and trend can be detected in a time series. It contains three components’ Trends, Seasonality, Resid. Below show the seasonal decomposition of US Crude oil price and Nigeria crude oil price.

<img width="802" height="583" alt="image" src="https://github.com/user-attachments/assets/45a36ba7-7f94-42ee-81ac-da1f2eaf6f65" />
This is US Crude oil seasonal decomposition
This is the seasonal decomposition of US crude oil with a rising trend, revealing the underlying movements of the data point. The residual plot is centered more around zero, even though there are some scattered points which might indicate the presence of noise. Looking at the seasonal plot, there is a little variation of seasonality but can be ignored. 


<img width="940" height="427" alt="image" src="https://github.com/user-attachments/assets/b1623ffb-7ac0-4ad6-a79c-54f3d76763d7" />
This is Nigeria crude oil seasonal decomposition
It reveals the underlying and behaviors of the components in the time series. The trend shows a downward movement while the residual varies in the region of -150 to 200. There is an obvious seasonality presence in the seasonal plot. This will impact the model to be considered when predicting. 


Anomaly Detection 
I checked for anomalies in the dataset by using different testing processes like Z-score to detect anomalies. Outliers are often seen as anomalies due to how they can negatively affect the performance of models and negate the forecasting results. So, it is necessary to resolve outliers impact before applying models. 

<img width="809" height="388" alt="image" src="https://github.com/user-attachments/assets/16632ac3-3612-422c-b433-4312a2737405" />
Detection of Outliers

<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/1dacd619-5729-477f-bd5b-75270bcc2a95" />
US crude oil price time series 
It represents a time series of united state crude oil prices from 2000 to 2023. The plot roughly starts from a downward trend at $30 per barrel till 2002 when the upward trend began at $20 per barrel. The upward trend reached $140 per barrel in May 2008 before experiencing another downward trend till Dec 2008 at $42 per barrel


<img width="975" height="504" alt="image" src="https://github.com/user-attachments/assets/432bd2f5-a156-4885-a063-5857d3588692" />
Nigeria CrudeOil Price and Rainfall measure in millimeter rain-gauge
represents time series of crude oil and rainfall in Nigeria between 2010 to 2023. The crude oil price fluctuated between the range 1500 to 1850 from 2010 to 2013. It took a major downward trend between 2016 to 2017 reaching a price of 1250. It then took an upward trend which did not last. In year 2018, it took a downward trend reaching a price of 900 in the year 2022 Q3. The Nigeria crude oil experience a lot of upward and downward trend during this period.

<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/b90181ff-0307-40f7-8b25-21d7dd5be960" />
Nigeria Rainfall measure in millimeter rain-gauge
is the rainfall data, it seems to be more consistent with it crest and trough over the years. It is an event that occurs seasonally. During the year 2016-2019 the rainfall data reached a height of 250 in measurement. This is the highest rainfall experience during the period of this dataset. 


<img width="940" height="456" alt="image" src="https://github.com/user-attachments/assets/96fcf40e-7af3-407f-9d82-6bb742d2f16e" />
Crude oil price during the hurricane/storm experience of 2004-2008
is the US crude oil price between 2005 to 2008. This data visualization is necessary because the US experienced hurricanes in the years 2005, 2007-2008. The price could be seen to be on an upward trend till April 2008. 

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/31beef26-2e32-4354-8bee-9ca59075802b" />
US Wind Speed time series for year 2005
shows multiple datapoints crossing 74 mph which can be attributed to hurricane occurrence. The 74 mph is the threshold for measuring how dangerous a wind speed can be. This is arguably the worst storm experience in US history called Hurricane katrina

# Correlation Test of Crude oil and Rainfall
<img width="940" height="520" alt="image" src="https://github.com/user-attachments/assets/2785cdb5-a656-4d6f-87a4-92d30d9fca28" />
There exists a weak correlation (0.12) between the CrudeOil and Rainfall time series. It shows that the relationship between them is weak, as it is measured from 0 to 1 as positive.

# Stationarity
The stationarity of the data is tested using ADF.
If the p-value is less than 0.05 the data is considered stationary
If the p-value is greater than 0.05 the data is considered non-stationary 
The p-value gave a number greater than 0.05, which implies that the test failed to reject the null hypothesis – it is non-stationary. 

<img width="940" height="83" alt="image" src="https://github.com/user-attachments/assets/cd7c4ed9-3a51-4028-a2b8-718ed7bbc9fe" />
US CrudeOil Fail to Reject null hypothesis

<img width="940" height="104" alt="image" src="https://github.com/user-attachments/assets/16c352e1-7108-40cc-b16c-2bffd39f1299" />
Nigeria CrudeOil Fail to Reject null hypothesis

# Differencing
This was applied because the dataset was initially non-stationary after using ADF test. The first step in applying differencing is using the First Differencing, which means subtracting the previous values from the current values. This way this data can achieve stationarity.

<img width="940" height="100" alt="image" src="https://github.com/user-attachments/assets/e0df99da-1982-42dd-9cff-7b6a39bf75a6" />
US Crude oil first differencing

<img width="940" height="89" alt="image" src="https://github.com/user-attachments/assets/16110aba-efd3-4fff-b0f1-930e97c9ee60" />
Nigeria CrudeOil First differencing 

# Autocorrelation and Partial Autocorrelation
Autocorrelation function (ACF) and the partial autocorrelation functions (PACF) plots are necessary for deriving the parameters value.

<img width="940" height="321" alt="image" src="https://github.com/user-attachments/assets/bf319078-8a68-4066-ade3-334df13aad5e" />
Autocorrelation of Nigeria crude oil
represent autocorrelation at zero is 1, this is because the time series is drawn to itself. Lag 1,3 reveals a negative correlation while lag 2, 4 shows a positive correlation


<img width="940" height="317" alt="image" src="https://github.com/user-attachments/assets/e085886d-7e54-40f4-9378-982d2294f5ac" />
Partial Autocorrelation of Nigeria crude oil
shows PACF is helpful in discovering the order of autoregressive (AR). It helps us identify the number of lagged observations in the model. AR is shown as (p) in ARIMA model. In a PACF, the first lag that is statistically significant ought to be the (p), this is whether the lag is positive or negative. 


# Endogenous and Exogenous
This project work will be applying the methodology of multiple time series application to measure the effect of one time series over other time series. This process will involve: one variable acting as a dependent while the other as independent. To be considered Endogenous variable, its value will be determined by other variables. In this case, crude oil price will be the Endogenous variable while Rainfall will be the Exogenous variable, whose impact will be measured on the value of Endogenous variable. 


# Implementing SARIMA
The SARIMA model was trained with 70% of the dataset (crude oil price) and 30% of the test data as shown in Fig 19 to understand the underlying facts about the crude oil price in Nigeria over some time.

<img width="975" height="440" alt="image" src="https://github.com/user-attachments/assets/353ce5f3-2805-4bdf-9e23-2beba310b865" />

# Implementing PROPHET Model
It works best with time series that have strong seasonal effects and several seasons of historical data. Prophet is robust at missing data and shifts in the trend, and typically handles outliers well (Facebook, 2023).

<img width="975" height="306" alt="image" src="https://github.com/user-attachments/assets/1e56383c-73cc-406b-83c0-36248ffa6a38" />


# Prediction

<img width="975" height="513" alt="image" src="https://github.com/user-attachments/assets/4a87d8b0-4102-4814-adb4-40ac156dd840" />

represents the prediction of crude oil prices in Nigeria. Vertical axis of the plot is the price in Naira while the horizontal axis is the years. The blue line is the training data. The red line is the predicted price, while the orange line represents the actual price (test data). The shaded area in the plot is the uncertainty band, which represents the scope the predicted data are expected to fall with a certain level of confidence. The lowest price on the train data is N1200 while the highest crude oil price in Nigeria is N1900. So, N700 is the difference between the highest and lowest crude oil price.  From the predicted values, the highest price is 1670.21 while the lowest price 1331.79.

# Granger Causality Test
This test is used to determine if a variable can be used to predict another variable in a time series. In this case, rainfall and crude oil prices. The Granger causality test is to prove the existence of likelihood of impact between independent and dependent variable at different time (t). This impact might not be immediate eg the impact of rainfall on crude oil prices might not happen immediately but can build up to cause a major disruption.

<img width="940" height="768" alt="image" src="https://github.com/user-attachments/assets/a65a79c7-5951-43a1-80c0-93c837ba0509" />
Granger Causality Test of Nigeria crude oil prices with Rainfall


# Reason Behind Different Lag Test
Testing different time (t) can signal the strongest time which the independent variable has predictive power on the dependent variable.

<img width="761" height="344" alt="image" src="https://github.com/user-attachments/assets/137345ec-1661-412a-9e02-890c73adbfdb" />
<img width="975" height="294" alt="image" src="https://github.com/user-attachments/assets/27029665-170e-42c3-8baf-78e41e225a0f" />
shows how exogenous variable (Rainfall) are applied on the endogenous variable (crude oil price). The variable rainfall is introduced to the SARIMAX model at lag 2 based on the Granger causality Test to see the influence of Rainfall on crude oil prices.

# Model Forecast
Forecasting is not guessing but rather a technique that uses historical data to make informed decisions about future events.

<img width="975" height="504" alt="image" src="https://github.com/user-attachments/assets/eb05c1d9-6680-46dd-9c5c-c4490292a21c" />
Forecasting Nigeria Crude Oil Prices with light Rainfall
the blue line is the real dataset, the red line represents the forecasted prices and orange is predicted prices. The confidence interval gets wider as the model predict into future. This simply means the deeper the model goes into the future the less reliable the price.


<img width="975" height="602" alt="image" src="https://github.com/user-attachments/assets/44a78456-a865-436a-b185-2ca4d7ac25bd" />
SARIMA model Crude oil prices with Light and Heavy Rainfall Forecast
shows different prices of crude oil when light and heavy rainfall was applied. The highest prices of crude oil with heavy rainfall is 1661 Naira while light rainfall is 1723 Naira. This simply means the higher the rainfall the more the prices fall. Ideally, the price ought to increase as the rainfall increases due to damages that this event will cause which will in turn makes crude oil to be scarce and expensive. This result might be due to inaccurate dataset or failure of the model to understand some basic patterns


# Prophet Prediction and Forecast

<img width="975" height="508" alt="image" src="https://github.com/user-attachments/assets/cc1e5a63-9024-48d3-a506-d9dd6a3bdd21" />
is the plot from prophet model. The plot shows the actual values in blue line and the orange line is split into two: Predict values and forecast values. The red line is where the forecast started. The forecast is a two-year event.


<img width="975" height="515" alt="image" src="https://github.com/user-attachments/assets/d75b0309-c625-40c9-9114-4c7b2510b44c" />
Prophet model forecast with light vs heavy rainfall impact
shows the result of impact of light and heavy rainfall on crude oil prices. The red line is the end of the actual data. The forecast is a quarterly event, so it is appropriate to see the forecast start around January 2024 since the dataset in used end in October 2023. The prophet model shows heavy rainfall forecasting a higher crude oil price while a light rainfall shows a lower crude oil price compared to heavy rainfall.

# Model Evaluation

Ljung-Box test
The Ljung-Box test is a test of “lack of fit” - if the autocorrelations of the residuals are very small, we say that the model doesn't show a “significant lack of fit”. This is good for the model as it proves model adequacy and is independent of residuals.

<img width="940" height="390" alt="image" src="https://github.com/user-attachments/assets/01b9b7fd-a245-47d9-8766-3fdcd98829ef" />
Histogram of Nigeria crude oil Residual plot without Rainfall impact

<img width="975" height="410" alt="image" src="https://github.com/user-attachments/assets/63f16cea-671f-4f9e-9f96-10638112ba38" />
Histogram of Nigeria crude oil Residual plot with Rainfall impact

# SARIMA and PROPHET Model 

	MAE	RMSE	MAPE
PROPHET	136.51	162.16	9.70
SARIMA	215.63	261.42	19.19

represents the performance evaluation of SARIMA model with rainfall with MAPE of 19.19% while Prophet model with rainfall is 9.70%. The model with lower MAPE clearly shows a better performance. This simply means the Prophet model understood the underlying pattern of the dataset than the SARIMA model.


# Conclusion
Through time Series Analysis on natural disaster impact on the economy, early recession can be detected in Nigeria. This study provided information into the seasonal variation of crude oil prices, a major contributor to the Nigeria’s GDP. Also, the insights of one of the major natural disasters in Nigeria, flooding, was highlighted through the trend of rainfall. These highlights help to measure the impact of flooding on crude oil prices, which can be a precursor to foretelling the likelihood of recession in the country. Furthermore, this study shows the importance of robust climatic and oil price datasets in getting accurate predictions








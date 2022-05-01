# Unit 10 - A Yen for the Future

![image](https://user-images.githubusercontent.com/99091066/166158554-b7978a08-1d7f-4fc4-8af2-1810b9f00f5a.jpeg)

This project aims to analyze the movements in the value of the Canadian dollar compares to the Japanese yen.

Using the historical CAD-JPY exchange rate [data](https://github.com/AmiraAli23/Time-Series/blob/b21ce2716b3864b392d8a299ee14875ef1653915/cad_jpy.csv), we performed time series forecasting and linear regression modelling to draw conclusions regarding the two currencies.


# Time Series Forecasting

After importing the data and trimming it to only include dates after 1990, we plot the "Price".

<img width="233" alt="Screen Shot 2022-05-01 at 2 10 03 PM" src="https://user-images.githubusercontent.com/99091066/166158832-0a0b8fd0-a70a-4324-8ac8-be7d64b0e1cb.png">

<img width="286" alt="Screen Shot 2022-05-01 at 2 10 18 PM" src="https://user-images.githubusercontent.com/99091066/166158841-50055c8d-463c-41e1-acf8-fd6361ed9646.png">

Long term, you will notice that the spikes last on average for three years before dipping back down. After 1996, there were no major dips and overall we can observe that the Japanese Yen has been strengthening overtime in value, against the Canadian dollar.

## Decomposition Using a Hodrick-Prescott Filter

We apply the Hodrick-Prescott filter by decomposing the exchange rate price into two series : price trend and price noise.


<img width="409" alt="Screen Shot 2022-05-01 at 2 20 53 PM" src="https://user-images.githubusercontent.com/99091066/166159148-a98a717d-0666-4ccd-b8e5-2bf62b3c14c5.png">


Using this data and combining it with the original dataframe, we plot the exchange rate price vs trend for 2015 to present.


<img width="587" alt="Screen Shot 2022-05-01 at 2 22 38 PM" src="https://user-images.githubusercontent.com/99091066/166159208-6c3f033b-ad58-4216-9998-b44faa5cabc1.png">

From 2015 to 2017, there was a consistent decrease in the price and trend. From 2017 to 2020, it remained consistent at around 80-85 CAD/JPY and dips again after 2020, which could be attributed to the global pandemic. For the most part, the prices are following the trends except for certain times in 2016-2017.

<img width="616" alt="Screen Shot 2022-05-01 at 2 32 03 PM" src="https://user-images.githubusercontent.com/99091066/166159531-006ae105-9d15-471d-a30e-d049787a7bcd.png">


We also plot the noise.


<img width="524" alt="Screen Shot 2022-05-01 at 2 35 04 PM" src="https://user-images.githubusercontent.com/99091066/166159669-9e0a1cd7-1f4a-45d1-aa5a-9a39c8ad3143.png">

There was a lot of noise around 2008, which alligns with the dip in price around the same time.


<img width="434" alt="Screen Shot 2022-05-01 at 2 37 51 PM" src="https://user-images.githubusercontent.com/99091066/166159784-b0df8baf-62c7-45fe-a7d1-0e31166b7185.png">

## Forecasting Returns using an ARMA (Autoregressive Moving Average) Model


<img width="421" alt="Screen Shot 2022-05-01 at 2 45 40 PM" src="https://user-images.githubusercontent.com/99091066/166160021-cf9650b0-1fdf-4d85-b90f-0e994754a19b.png">

<img width="363" alt="Screen Shot 2022-05-01 at 2 58 14 PM" src="https://user-images.githubusercontent.com/99091066/166160454-7a97c6a6-e894-4173-bcd3-315dbf9e9d0d.png">

Given that a p-value < 0.05 indicates a good fit, this model is not a good fit as it exceeds that threshold.

## Forecasting the Exchange Rate Price using an ARIMA Model

<img width="368" alt="Screen Shot 2022-05-01 at 3 03 45 PM" src="https://user-images.githubusercontent.com/99091066/166160627-0f877036-b658-4fda-b0ff-bd70e7d65da9.png">


<img width="334" alt="Screen Shot 2022-05-01 at 3 04 31 PM" src="https://user-images.githubusercontent.com/99091066/166160651-2c77468b-0859-4e74-9efc-2c7a580d870a.png">

The ARIMA model predicts a decrease in price for the five day futures.

## Volatility Forecasting with GARCH

<img width="368" alt="Screen Shot 2022-05-01 at 3 07 29 PM" src="https://user-images.githubusercontent.com/99091066/166160754-280ce3ac-d71c-402d-9d75-373d681cbb8c.png">

We create a five day forecast of volatility and plot the figure.


<img width="372" alt="Screen Shot 2022-05-01 at 3 09 12 PM" src="https://user-images.githubusercontent.com/99091066/166160827-cd64deaa-46a2-4b2e-aea3-8bc38c83a7de.png">


<img width="344" alt="Screen Shot 2022-05-01 at 3 08 51 PM" src="https://user-images.githubusercontent.com/99091066/166160811-a03c41b2-7ce5-49e0-b509-2678c7fa48c6.png">


The model predicts a consistent increase in volatility over the next five days, the slope of the curve is around a perfect 1.

## Conclusions for Time Series

Based on our time series analysis, I would not purchase the yen now as the models predict lower prices and higher volatilities. However, the general trend is that the Yen is strengthening against the Canadian dollar. I would not purchase the Yen for short term opportunities and would consider a long term position instead.

The risk of the Yen is expected to increase given our results from the GARCH model.

I would not feel confident with these models for training since the p values are above 0.05 and the five day return forecast are very unstable/ fluctuating for a short time frame.


# Regression Analysis: Seasonal Effects with Sklearn Linear Regression


## Data Preparation

Using the same data from the first section, we add a `Price_Return` column that calculates the price returns and a `Lagged_Return`column.

<img width="346" alt="Screen Shot 2022-05-01 at 3 26 59 PM" src="https://user-images.githubusercontent.com/99091066/166161511-9af7ac9b-f0c9-4716-b239-d5932fa61f38.png">

<img width="429" alt="Screen Shot 2022-05-01 at 3 28 09 PM" src="https://user-images.githubusercontent.com/99091066/166161550-3a6fe03c-9aa7-4c8c-8fc3-2c8b9108083f.png">

## Linear Regression Model

```` python 
from sklearn.linear_model import LinearRegression

#regress = LinearRegression().fit(x_train, y_train)
reg= LinearRegression()
reg.fit(x_train,y_train)

```` 

## Make predictions using the Testing Data


<img width="371" alt="Screen Shot 2022-05-01 at 3 30 27 PM" src="https://user-images.githubusercontent.com/99091066/166161623-93bab1c4-7a9d-4754-b3e6-7470408b8369.png">


## Out-of-Sample / In-Sample  Performance

Mean Squared Error

`MSE` Testing Data : 0.415484105880405
`MSE` Training Data : 0.708954961822499

Root Mean Squared Error

`RMSE` Testing Data : 0.6445805658569028
`RMSE` Training Data : 0.841994632894117

The model performs better with training (in-sample) data as the RMSE is 0.84199 compared to the testing (out-of-sample) data at 0.70895.













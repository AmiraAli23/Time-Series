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

## Forecasting Returns using an ARMA Model




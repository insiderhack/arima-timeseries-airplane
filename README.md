# Time Series Forecast : A basic introduction using Python.

Time series data is an important source for information and strategy used in various businesses. From a conventional finance industry to education industry, they play a major role in understanding a lot of details on specific factors with respect to time.

Time series forecasting is basically the machine learning modeling for Time Series data (years, days, hours…etc.)for predicting future values using Time Series modeling .This helps if your data in serially correlated. Loading and Handling Time Series in Pandas.

I will be using python in jupyter notebook. Pandas in python has libraries that are specific to handling time series object .

Let's start with the Preliminaries
```
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
%matplotlib inline
```
To load the data- I have provided the link to my GitHub where the dataset and the code is available. I will be using the AirPassenger dataset from. Are you ready?
```
data = pd.read_csv('AirPassengers.csv')
print data.head()
print '\n Data Types:'
print data.dtypes
```
Looking at the output. The data contains a particular month and number of passengers travelling in that month .The data type here is object (month) Let’s convert it into a Time series object and use the Month column as our index.

```
from datetime import datetime
con=data['Month']
data['Month']=pd.to_datetime(data['Month'])
data.set_index('Month', inplace=True)
#check datatype of index
data.index
```
You can see that now the data type is ‘datetime64[ns]’.Now let’s just make it into a series rather than a data frame.

```
#convert to time series:
ts = data['#Passengers']
ts.head(10)

```
### STATIONARY

This is a very important concept in Time Series Analysis. In order to apply a time series model, it is important for the Time series to be stationary; in other words all its statistical properties (mean,variance) remain constant over time. This is done basically because if you take a certain behavior over time, it is important that this behavior is same in the future in order for us to forecast the series. There are a lot of statistical theories to explore stationary series than non-stationary series. (Thus we can bring the fight to our home ground!)

In practice we can assume the series to be stationary if it has constant statistical properties over time and these properties can be:
*Contant Mean
*Constant Variance
*An auto co-Variance that does'nt depend on time

These details can be easily retrieved using stat commands in python.
The best way to understand you stationarity in a Time Series is by eye-balling the plot:
```
plt.plot(ts)
```
It’s clear from the plot that there is an overall increase in the trend,with some seasonality in it.
I have written a function for it as I will be using it quite often in this Time series explanation. But before we get to that,let me explain all the concepts in the function.

Plotting Rolling Statistics :The function will plot the moving mean or moving Standard Deviation. This is still visual method
NOTE: moving mean and moving standard deviation — At any instant ‘t’, we take the mean/std of the last year which in this case is 12 months)

Dickey-fuller Test :This is one of the statistical tests for checking stationarity. First we consider the null hypothesis: the time series is non- stationary. The result from the rest will contain the test statistic and critical value for different confidence levels. The idea is to have Test statistics less than critical value, in this case we can reject the null hypothesis and say that this Time series is indeed stationary (the force is strong with this one !!)

Function details:
*Mean
*Standard deviation (instead of variance)
*Plot original series
*Plot mean
*Plot std
*Plot Dickey-Fuller test
```
from statsmodels.tsa.stattools import adfuller
def test_stationarity(timeseries):
    
    #Determing rolling statistics
    rolmean = pd.rolling_mean(timeseries, window=12)
    rolstd = pd.rolling_std(timeseries, window=12)
#Plot rolling statistics:
    plt.plot(timeseries, color='blue',label='Original')
    plt.plot(rolmean, color='red', label='Rolling Mean')
    plt.plot(rolstd, color='black', label = 'Rolling Std')
    plt.legend(loc='best')
    plt.title('Rolling Mean & Standard Deviation')
    plt.show()
    #Perform Dickey-Fuller test:
    print 'Results of Dickey-Fuller Test:'
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic','p-value','#Lags Used','Number of Observations Used'])
    for key,value in dftest[4].items():
        dfoutput['Critical Value (%s)'%key] = value
    print dfoutput
```

### for more details lets see the code below

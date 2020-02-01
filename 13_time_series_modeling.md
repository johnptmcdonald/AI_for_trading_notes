# Time series modeling

## What is an auto-regressive model?
An auto regressive model is one that uses observations from previous time steps as input to a regression equation to predict the value at the next time step. 

For example, if the usual regression equation is as follows:
```
y_hat = b0 + b1*X1
```

then the autoregressive version of this is as follows:
```
Xt = b0 + b1*X(t-1) + b2*X(t-2) ...
```
Because the model uses data from the input input variable at previous time steps, it is called an _auto_regression.

### Autocorrelation
An autoregressive model makes an assumption that the observations at previous time steps are useful to predict the value at the next time step, i.e. that there is some form of correlation (in this case _auto_correlation). We can check the amount of autocorrelation with an ACF (auto-correlation function) plot. This might overstate the autocorrelation of particular timesteps, so we should really do a PACF plot (partial ACF), which looks at each timestep more in isolation. 

We then do a *Ljung-Box* test to check whether a particular laggives autocorrelations that are significantly different from zero. 

In general, positive autocorrelation means there is momentum (good for monthly FX), whereas negative autocorrelation means there is mean reversion (good for weekly stocks). 


## What is a moving average model?
The moving average model should not be confused with the moving average itself. The moving average model specifies that the output variable depends linearly on the current and past values of a stochastic term. Rather than using past values of the forecast variable in a regression, a moving average model uses past forecast errors in a regression like model:
```
Xt = c + Et + theta1*E(t-1) + theta2*E(t-2) + theta3*E(t-3) ...
```
Where each `E` is a past forecast error (residual). It is not a regression in the usual sense because we do not observe the values of each `E`. In effect, each value of `Xt` can be thought of as the weighted moving average of the past forecast errors (residuals). 

We can model that the observations of a random variable at time
`t` are not only affected by the shock at time `t`, but also the shocks that have taken place before time `t`. For example, if we observe a negative shock to the economy, say, a catastrophic earthquake, then we would expect that this negative effect affects the economy not only for the time it takes place, but also for the near future. This kind of thinking can be represented by an MA model.

## What is the difference between an autoregressive and a moving average model?
in an AR model, the predicted value is calculated as a regression from previous values. in an MA model, the predicted value is calculated as a weighted moving average of past forecast errors. 

https://campus.datacamp.com/courses/machine-learning-for-time-series-data-in-python/time-series-and-machine-learning-primer?ex=1

## What is ARMA?
ARMA is a combination of AR and MA, which models the next step in the sequence as a linear function of the observations _and_ the residuals at prior time steps, so it says that the current return can be predicted by previous returns plus previous errors/'shocks' to the system. 

## So what is ARIMA?!
ARIMA is Autoregression Integrated Moving Average model. It is basically ARMA that includes a 'differencing' pre-processing step used to make the sequence stationary (this process is called integration)

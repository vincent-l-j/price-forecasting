# Price Forecasting

## Installation via [Anaconda](https://www.anaconda.com/products/individual)
```bash
# git clone this repo
cd path/to/price-forecasting
conda env create --file environment.yml
conda activate price_forecasting
```

## Background
The financial departments of large companies often have to make foreign currency transactions when doing international business, while hedge funds are also interested in anything that will provide an edge in predicting currency movements. Hence, both are always eager to gain a better understanding of the future direction and risk of various currencies. 

This analysis uses various time series tools to predict future movements in the value of the Canadian dollar versus the Japanese yen.

## Summary of Findings

### Time-Series Forecasting

In [time_series_analysis.ipynb](src/time_series_analysis.ipynb), time series analysis and modelling were used to determine if there is any predictable behaviour in the historical CAD-JPY exchange rate.

1. After plotting the Settle price, it can be seen from the lower highs that there is a long-term downtrend. In the mid to short-term, the exchange rate looks to be trading in a descending triangle.

2. After decomposing the settle price into trend and noise using a Hodrick-Prescott filter, it can be seen that there is a short-term uptrend.

3. Two ARMA models were used to forecast returns. The model of order (2,1) had 2 p-values less than 0.05 and the other 2 p-values greater than 0.05. The model of order (1,1) had 2 p-values less than 0.05 and the other p-value greater than 0.05. The model of (2,1) did not have significantly better AIC and BIC scores and thus the simpler model (1,1) is deemed better. Both models forecasted negative returns. Model (1,1) forecasted negative returns that were gradually becoming positive, whereas the other model was very volatile and forecasted returns that were becoming more negative.

4. Forecasting the exchange rate price using an ARIMA model suggested that the price of the Japanese Yen will rise with respect to the Canadian Dollar in the near term.

5. The GARCH model forecasted increased volatility in the near term.

6. Based on the time series analysis, it seems to be a good time to buy the yen for riskier investors.
7. Given that the volatility is likely to increase (GARCH model), the risk of the yen should be expected to increase.
8. Model evaluation and confidence in practical usage:
   1. Only 2 of the p-values in the ARMA model with order (2,1) are less than 0.05.
   2. All but 1 of the p-values in the ARMA model with order (1,1) are less than 0.05.
   3. None of the p-values in the ARIMA model are less than 0.05 and makes me doubt how well such a model will perform.
   4. The p-values for GARCH and volatility forecasts are much lower than the ARMA/ARIMA return and price forecasts. On the GARCH model, all p-values are less than 0.05, except for alpha(2), indicating a much better model performance. This makes me feel more confident about the GARCH's forecast than the other ones.
   5. However, since none of the models had all p-values less than 0.05, I would not feel confident using these models for trading significant amounts of money.

### Linear Regression Forecasting

In [regression_analysis.ipynb](src/regression_analysis.ipynb), a linear regression model was used to predict CAD/JPY returns with *lagged* CAD/JPY futures returns and categorical calendar seasonal effects (e.g., day-of-week or week-of-year seasonal effects).

- The Out-of-Sample Root Mean Squared Error (RMSE) is 0.6445805658569028
- The In-sample Root Mean Squared Error (RMSE) is 0.841994632894117
- This model performs better on out-of-sample data as compared to in-sample data.

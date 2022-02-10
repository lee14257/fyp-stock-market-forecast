# Deep Learning and Directional Stock Market Forecast
Directional stock market forecast using deep learning models

Models were trained via Google Cloud TPU, and its prediction outputs were used to form custom trade strategies that were simulated for NQ Mobile stocks.

## Data
The data represents daily stock price indicators of the NQ Mobile Inc. stock from the 2nd of September 1999 through to the 3rd of January 2018 depicting 4628 trading days across almost 10 years. NQ Mobile has since rebranded and is now tradable on the US stock market under the nameLink Motion.

| Technical Indicators | Description |
| --- | --- |
| Open | Stock price at market opening |
| High | Stock’s highest Price during the day |
| Low  | Stock’s lowest Price during the day |
| Close | Stock’s price at market closing |
| Volume | Number of shares traded during the given time period|
| MACD | Moving Average Convergence Divergence: displays characteristics of momentum and trend of a stock's price |
| MACDAvg | Moving Average Convergence Divergence Average: displays the exponential average of MACD |
| MACDDiff | Moving Average Convergence Divergence Difference: displays the difference between the MACD and MACDAvg |
| RSI | Relative Strength Index: represents a momentum indicator that measures the magnitude of recent price changes to evaluate overbought or oversold conditions in the price of a stock |
| SlowK | Slow Stochastic Oscillator: A momentum indicator that shows the location of the close relative to the high-low range over a set number of periods |
| CCI | Commodity Channel Index: helps find start and end of a trend |
| ATR | Average True Range: measures the volatility of price |
| BOLL | Bollinger Band: helps in pattern recognition, by providing a relative definition of high and low |
| EMA20 | 20 day Exponential Moving Average |
| SMI | Stochastic Momentum Index: shows where the close price is relative to the midpoint of the same range |
| WVAD | William’s Variable Accumulation Distribution: measures the buying and selling pressure |
| ROC | Rate Of Change: shows the speed at which the stock’s price is changing |


## Directional Predictions
The directional prediction of the next day’s stock price is determined by computing the change from the predicted stock price (t+1)’ to the stock price of the last day from the input time-series (t).

| Category| Criteria |
| --- | --- |
| Up | (t+1)’ ≥ 1.03% × t|
| No Change | 0.97% × t <(t+1)’<1.03% × t |
| Down | (t+1)’ ≤ 0.97% × t |


## Model Trading Strategies
- Strategy 1: On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and immediately sell on t+1. Otherwise, do nothing. 
- Strategy 2: On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and hold until the model predicts a "Down" on (t+1)+α. 

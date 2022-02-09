# Deep Learning and Directional Stock Market Forecast
Directional stock market forecast using deep learning models


## Data
The dataset used throughout our final year project in order to train and test our different deep learning models as well as compare our models’ outputs to common trading algorithms is the NQ Mobile Inc. stock. The data represents daily stock price indicators of the NQ Mobile Inc. stock from the 2nd of September 1999 through to the 3rd of January 2018 depicting 4628 trading days across almost 10 years. NQ Mobile has since rebranded and is now tradable on the US stock market under the nameLink Motion.

Another reason why we selected the NQ Mobile stock is because throughout the 10 years we can observe both an increase and decrease in stock price which will allow us to test our different trading strategies across mercurial trading environments

Below is the list of financial technical indicators included in the data set. However, through data preprocessing we will choose to eliminate or transform some of the metrics below.

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
| SlowD | Slow Stochastic Moving Average: the moving average of SlowK |
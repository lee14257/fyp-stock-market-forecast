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

## Models
- Convolutional Neural Network (CNN)
- Convolutional Sparse Coding (CSC)
- Temporal Convolutional Network / WaveNet (TCN)
- Bi-directional LSTM
- Bi-directional LSTM with Autoencoders

## Directional Predictions
The directional prediction of the next day’s stock price is determined by computing the change from the predicted stock price (t+1)’ to the stock price of the last day from the input time-series (t).

| Category| Criteria |
| --- | --- |
| Up | (t+1)’ ≥ 1.03% * t|
| No Change | 0.97% × t < (t+1)’ < 1.03% * t |
| Down | (t+1)’ ≤ 0.97% * t |

## Methodology
![alt text](/docs/methodology.png)

## Model Trading Strategies
#### Strategy 1 
On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and immediately sell on t+1. Otherwise, do nothing. 

![alt text](/docs/strategy-1.png)

#### Strategy 2 
On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and hold until the model predicts a "Down" on (t+1)+α. 

![alt text](/docs/strategy-2.png)

## Model Results
Mean directional accuracies for the 5 models' predictions on 3 price directions ("Up", "Down", "No Change") turned out to be higher than random guessing (33%).

| Metrics| CNN | CSC | TCN | Bi-LSTM | Bi-LSTM Autoencoders |
| --- | --- | --- | --- | --- | --- |
| MSE (Mean Squared Error) | 3071.1 | 1223.7 | - | 2297.1 | 3831.2 |
| MAPE (Mean Abs. Percentage Error) | 1.43% | 0.91% | - | 1.39% | 1.61% |
| MDA (Mean Directional Accuracy) | 41.15% | 46.75% | 40.79% | 41.32% | 40.37% |

## Simulation Results
Stock market for NQ Mobile Inc. was simulated for 2 periods of time:
- Period 1: 18/01/2007 - 30/10/2008
- Period 2: 11/03/2016 - 29/12/2017

The 2 strategies were applied to the model prediction outputs, and the Total Cumulative Daily Returns (%) was measured and compared.

![alt text](/docs/period-1-strategy-1.png)

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 71.1% |
| Bi-directional LSTM + auto | 41.7% |
| Bi-directional LSTM | 12.1% |
| CSC | 6.2% |
| CNN | -0.01% |
| Buy and Hold | -40.3% |

![alt text](/docs/period-1-strategy-2.png)

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 37.0% |
| Bi-directional LSTM + auto | 31.3% |
| Bi-directional LSTM | 6.3% |
| CSC | 8.3% |
| CNN | 0% |
| Buy and Hold | -40.3% |

![alt text](/docs/period-2-strategy-1.png)

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 35.1% |
| Bi-directional LSTM + auto | 25.4% |
| Bi-directional LSTM | 20.4% |
| CSC | 22.2% |
| CNN | 20.1% |
| Buy and Hold | 40% |

![alt text](/docs/period-2-strategy-2.png)

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 45.6% |
| Bi-directional LSTM + auto | 25.7% |
| Bi-directional LSTM | 16.0% |
| CSC | 30.3% |
| CNN | 31.2% |
| Buy and Hold | 40% |



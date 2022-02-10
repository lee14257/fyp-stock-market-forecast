# Deep Learning and Directional Stock Market Forecast
> This project explores various novel deep learning models in the context of directional stock market forecast and evaluates their performances in a simulated market. The models were trained via Google Cloud TPU, and its prediction outputs were used to form custom trade strategies to compare against a base real-life buy and hold strategy.

## Data
The data represents daily stock price indicators of the NQ Mobile Inc. stock from the 2nd of September 1999 through to the 3rd of January 2018 depicting 4628 trading days across almost 10 years. NQ Mobile has since rebranded and is now tradable on the US stock market under the name Link Motion.

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

## Directional Prediction Criteria
The directional prediction of the next day’s stock price is determined by computing percentage changes from the predicted stock price (t+1)’ to the previous day stock price (t) of the time series.

| Category| Criteria |
| --- | --- |
| Up | (t+1)’ ≥ 1.03% * t|
| No Change | 0.97% × t < (t+1)’ < 1.03% * t |
| Down | (t+1)’ ≤ 0.97% * t |

## Methodology
<img src="/doc/methodology.png" width="600" height="680">

## Model Trading Strategies
#### Strategy 1 
On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and immediately sell on t+1. Otherwise, do nothing. 

<img src="/doc/strategy-1.png" width="430" height="500">

#### Strategy 2 
On day t, if the model predicts "Up" on day t+1, then buy the stock on day t and hold until the model predicts a "Down" on (t+1)+α. 

<img src="/doc/strategy-2.png" width="500" height="600">

## Model Results
Mean directional accuracies for the 5 models' predictions on 3 price directions ("Up", "Down", "No Change") turned out to be higher than random guessing (33%).

| Metrics| CNN | CSC | TCN | Bi-LSTM | Bi-LSTM Autoencoders |
| --- | --- | --- | --- | --- | --- |
| MSE (Mean Squared Error) | 3071.1 | 1223.7 | - | 2297.1 | 3831.2 |
| MAPE (Mean Abs. Percentage Error) | 1.43% | 0.91% | - | 1.39% | 1.61% |
| MDA (Mean Directional Accuracy) | 41.15% | 46.75% | 40.79% | 41.32% | 40.37% |

## Simulation Results
Stock market for NQ Mobile Inc. was simulated for 2 periods of test time frames:
- **Period 1**: 18-Jan-2007 to 30-Oct-2008
- **Period 2**: 11-Mar-2016 to 29-Dec-2017

The 2 strategies were applied to the model prediction outputs, and the Total Cumulative Daily Returns (%) was measured and compared.

### Period 1 + Strategy 1

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 71.1% |
| Bi-directional LSTM + auto | 41.7% |
| Bi-directional LSTM | 12.1% |
| CSC | 6.2% |
| CNN | -0.01% |
| Buy and Hold | -40.3% |

![alt text](/doc/period-1-strategy-1.png)


### Period 1 + Strategy 2

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 37.0% |
| Bi-directional LSTM + auto | 31.3% |
| Bi-directional LSTM | 6.3% |
| CSC | 8.3% |
| CNN | 0% |
| Buy and Hold | -40.3% |

![alt text](/doc/period-1-strategy-2.png)


### Period 2 + Strategy 1

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 35.1% |
| Bi-directional LSTM + auto | 25.4% |
| Bi-directional LSTM | 20.4% |
| CSC | 22.2% |
| CNN | 20.1% |
| Buy and Hold | 40% |

![alt text](/doc/period-2-strategy-1.png)


### Period 2 + Strategy 2

| Models | Cumulative Daily Returns |
| --- | --- |
| TCN | 45.6% |
| Bi-directional LSTM + auto | 25.7% |
| Bi-directional LSTM | 16.0% |
| CSC | 30.3% |
| CNN | 31.2% |
| Buy and Hold | 40% |

![alt text](/doc/period-2-strategy-2.png)



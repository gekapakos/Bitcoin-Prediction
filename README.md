# Project Overview

## Bitcoin Price Prediction
- **Description**: A neural network-based project forecasting daily Bitcoin prices (USD) using ARIMA and LSTM models. Analyzes minute-level data from Jan 1, 2021, to Mar 1, 2022, targeting price trends and absolute values.
- **Purpose**: Aims to predict Bitcoin’s volatile price movements for financial insights, comparing statistical and deep learning approaches.
- **Team**: Dimitrios Tsalapatas (03246), Ioannis Reinos (03390), Eleni Athanailidi (03453), Georgios Kapakos (03165).
- **Institution**: Electrical and Computer Engineering, University of Thessaly, Volos, Greece.

## Dataset
- **Source**: Bitcoin price data (BTC/USD) with minute-level granularity.
- **Features**: Date, Open, High, Low, Close, Volume (BTC/USD).
- **Period**: Jan 1, 2021, 12:01 AM - Mar 1, 2022, 3:43 AM.

## Preprocessing
- **Steps**:
  - Converted date to datetime, sorted chronologically.
  - Dropped `unix`, `symbol`, `Volume BTC/USD`.
  - **Impl. 1**: MinMax-scaled `Close` per minute (R²=0.99).
  - **Impl. 2**: Daily average `Close` (R²=0.21).
  - **Impl. 3**: Price change (`Next Close - Close`) with lag features (1-3), rolling means (5, 10, 15), RSI, EMA, MACD (R²=-0.0036).
  - Missing values filled with means, outliers handled via IQR.

## Models
- **ARIMA (0,1,1)**: 
  - Stationarized with first-order differencing.
  - R²=-2.27, RMSE=1889.85, MAE=1584.23.
- **LSTM**: 
  - 50-unit layer, ReLU, Dense output, Adam optimizer, MSE loss.
  - **Impl. 1**: R²=0.99, RMSE=0.0015, MAE=0.0012, 10 epochs, 677s.
  - **Impl. 2**: R²=0.21, RMSE=0.045, MAE=0.034, 100 epochs, 18.9s.
  - **Impl. 3**: R²=-0.0036, RMSE=277.42, MAE=181.93, 50 epochs, 358s.

## Evaluation
- **Metrics**: RMSE, MAE, MAPE, R².
- **Findings**: LSTM (Impl. 1) excels in absolute price prediction but less relevant economically. Impl. 3 (price change) aligns with trends but underperforms. ARIMA fails to capture volatility.

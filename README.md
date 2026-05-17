# Apple Closing Price Prediction Model

<img width="911" height="463" alt="apple-stock-project" src="https://github.com/user-attachments/assets/4deb114e-9141-4e72-b14a-2d17f04360f2" />

A deep learning model that uses a **Long Short-Term Memory (LSTM)** to predict the closing stock price of Apple Inc. (AAPL).

## Overview

The model uses daily AAPL closing prices going back to January 2016. For 80% of the data, the model trains using a rolling 60-day window as input to predict the next day's closing price scaled to [0, 1]. 
This is then tested with the remaining 20%, where it produced results to an RMSE of 4.14.

## Results

| Metric | Value |
|--------|-------|
| RMSE (held-out test set) | **4.14** |

## Model Architecture

Built with Keras Sequential API:

| Layer | Units | Notes |
|-------|-------|-------|
| LSTM | 50 | `return_sequences=True` |
| LSTM | 50 | `return_sequences=False` |
| Dense | 25 | |
| Dense | 1 | Output — predicted closing price |

- **Optimizer:** Adam  
- **Loss:** Mean Squared Error  
- **Input shape:** (60 timesteps, 1 feature)

## Tech Stack

- Python
- [yfinance](https://github.com/ranaroussi/yfinance) — historical stock data
- Pandas / NumPy — data manipulation
- Scikit-Learn — Min-Max scaling
- Keras / TensorFlow — LSTM model
- Matplotlib — visualisation

## Usage

1. Clone the repo and open the notebook in [Google Colab](https://colab.research.google.com) or Jupyter.
2. Install dependencies:
   ```bash
   pip install yfinance pandas numpy scikit-learn keras matplotlib
   ```
3. Run all cells. The notebook will:
   - Download live AAPL data via `yfinance`
   - Train the LSTM on 80% of the data
   - Plot training history vs. validation predictions
   - Print the RMSE and a next-day price prediction

## Visualisations

The notebook produces two plots:
- **Close Price History** — full historical closing price of AAPL
<img width="911" height="464" alt="image" src="https://github.com/user-attachments/assets/0183ba9e-eda0-4712-8186-c3a234ca7f6e" />

- **Model Output** — training data, actual validation prices, and model predictions overlaid
<img width="911" height="463" alt="apple-stock-project" src="https://github.com/user-attachments/assets/4deb114e-9141-4e72-b14a-2d17f04360f2" />

## Notes

- The model is trained for a single epoch by default for speed; increasing `epochs` will generally improve accuracy at the cost of training time.
- Predictions are generated for the most recent 60 days available at runtime, so results will vary depending on when the notebook is run.

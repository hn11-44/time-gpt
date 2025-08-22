# Nixtla Ecosystem Exploration

![Nixtla Logo](https://raw.githubusercontent.com/Nixtla/neuralforecast/main/nbs/imgs/logo_black.png)

This repository is dedicated to exploring, testing, and experimenting with the powerful time-series forecasting libraries developed by [Nixtla](https://nixtla.io/). The primary goal is to understand the capabilities, performance, and nuances of each package through practical examples, benchmarks, and hands-on coding.

## 🎯 Objective

The main objectives of this project are:
-   To gain a deep understanding of Nixtla's core libraries for time series analysis.
-   To compare the performance and ease of use of different models (`statsforecast`, `mlforecast`, `neuralforecast`).
-   To experiment with feature engineering, model tuning, and evaluation techniques within the Nixtla framework.
-   To serve as a personal knowledge base and a collection of practical code snippets for future time series projects.

## 📊 Datasets of Focus

Our primary experiments will revolve around real-world, high-frequency energy datasets to test the scalability and accuracy of Nixtla's models under challenging conditions. The initial focus will be on:

-   **Italian Electricity Market:** Analyzing load and price data.
-   **Spanish Electricity Market:** Forecasting demand and generation.

*Note: The repository structure is currently under construction and will be defined as the project progresses.*


## 📚 Packages of Interest

We are focusing on the following libraries from the Nixtla ecosystem:

-   **StatsForecast:** Lightning-fast and scalable library for classical statistical time series forecasting models like ARIMA, ETS, and Theta.
-   **MLForecast:** Scalable machine learning for time series forecasting, allowing the use of models like LightGBM, XGBoost, and Scikit-Learn regressors.
-   **NeuralForecast:** A user-friendly library for state-of-the-art deep learning models for time series forecasting, including N-BEATS, N-HiTS, and PatchTST.
-   **TimeGPT:** The first foundation model for time series, offering powerful zero-shot forecasting capabilities through a simple API.

## 🚀 Getting Started

This project uses `uv` for fast and efficient package management.

### Prerequisites

-   Python 3.8+
-   uv installed. You can install it with:
    ```bash
    # On macOS and Linux
    curl -LsSf https://astral.sh/uv/install.sh | sh

    # On Windows
    powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```

### Installation

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd TimeGpt
    ```

2.  **Create a virtual environment and install dependencies:**
    `uv` can handle both creating the environment and installing packages.
    ```bash
    # Create a virtual environment named .venv
    uv venv

    # Activate the environment
    source .venv/bin/activate  # On Windows, use `.venv\Scripts\activate`

    # Install packages from requirements.txt
    uv pip install -r requirements.txt
    ```

## 💻 Usage

The core of this project lies in the `notebooks/` directory. Each Jupyter Notebook is a self-contained experiment focusing on a specific library or model.

1.  Start Jupyter Lab or Jupyter Notebook:
    ```bash
    jupyter lab
    ```
2.  Navigate to the `notebooks/` directory and open a notebook to start exploring.

### Quick Example (`StatsForecast`)

Here is a small snippet to demonstrate the simplicity of getting a forecast with `StatsForecast`.

```python
import pandas as pd
from statsforecast import StatsForecast
from statsforecast.models import AutoARIMA

# Create a sample DataFrame in the required format
# 'unique_id' identifies the time series
# 'ds' is the timestamp
# 'y' is the target variable
df = pd.DataFrame({
    'unique_id': ['T1'] * 50,
    'ds': pd.to_datetime(pd.date_range('2023-01-01', periods=50, freq='D')),
    'y': [i + 2 * (i%7) for i in range(50)] # Some dummy data with weekly seasonality
})

# Define models and forecast horizon
models = [AutoARIMA()]
sf = StatsForecast(
    df=df,
    models=models,
    freq='D',
    n_jobs=-1  # Use all available cores
)

# Generate a 14-day forecast
forecast_df = sf.forecast(h=14)

print(forecast_df.head())
```

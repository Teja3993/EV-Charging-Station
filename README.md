# ⚡ Grid-Aware EV Charging Demand Forecasting

## 📖 Overview
This repository contains a machine learning pipeline that predicts future hourly Electric Vehicle (EV) charging demand in kilowatts (kW). 

Unlike standard time-series models that rely solely on historical clock patterns, this model is **"grid-aware."** It factors in real-time power grid conditions, such as carbon intensity and renewable energy availability, to make its predictions. This repository serves as a portfolio piece and the foundation for a technical research paper.

## 🛠️ Data Engineering & Leakage Resolution
The model is built on a California charging station dataset. A major focus of this project was debugging data leakage to ensure the model reflects a strict, real-world deployment scenario.

* **Identifying Leaks:** Initial baseline models produced artificially high scores. Through feature importance analysis and decision tree visualization, target-dependent variables were identified and removed (e.g., `Peak Demand (kW)`, `Number of EVs Charging`, `Grid Stability Index`).
* **Temporal Feature Engineering:** Created 1-hour and 24-hour demand lag features, and converted the hour of the day into cyclical sine/cosine variables to capture daily charging rhythms.

## 🏆 Model Performance
Three regression models (Linear Regression, XGBoost, and Random Forest) were tested and validated using a 5-fold `TimeSeriesSplit` to prevent the models from looking ahead in time. 

The champion model, a **RandomForestRegressor**, demonstrated exceptional performance on the unseen hold-out test set:

| Metric | Score | Interpretation |
| :--- | :--- | :--- |
| **RMSE** (Root Mean Squared Error) | **0.0129 kW** | The model's predictions have a very low typical error magnitude. |
| **MAE** (Mean Absolute Error) | **0.0107 kW** | On average, the model's prediction is off by only 0.01 kW. |
| **R-squared ($R^2$)** | **0.9777** | The model successfully explains **97.8%** of the variance in charging demand. |

## 🧠 Key Insights (Feature Importance)
A SHAP/Feature Importance analysis proved that the model successfully learned grid dynamics rather than just memorizing the clock. The top three predictors for EV charging demand were:
1. **Carbon Emissions ($kgCO_2/kWh$)**
2. **Previous Hour Demand (lag_1hr)**
3. **Renewable Energy Usage (%)**

This establishes a strong, quantifiable relationship between user charging behaviors and the active state of the power grid.

## 💻 Technology Stack
* **Language:** Python 3.10+
* **Machine Learning:** Scikit-Learn, XGBoost
* **Data Processing:** Pandas, NumPy
* **Visualization:** Matplotlib, Seaborn

## 🚀 Getting Started

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Teja3993/EV-Charging-Station.git](https://github.com/Teja3993/EV-Charging-Station.git)
    cd EV-Charging-Station
    ```
2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    # On Windows: venv\Scripts\activate
    # On Mac/Linux: source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install pandas numpy scikit-learn xgboost matplotlib seaborn
    ```
4.  **Run the pipeline:**
    * Execute the data merging script to combine the raw CSV files.
    * Launch JupyterLab to view the modeling notebook, preprocessing steps, and final evaluation plots.

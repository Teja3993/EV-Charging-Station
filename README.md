# EV Charging Demand Forecast: A Time-Series ML Project


## 📖 Overview

This project presents an end-to-end machine learning workflow to forecast Electric Vehicle (EV) charging demand using a time-series dataset from California. The primary goal was to analyze historical data, engineer relevant features, and build a highly accurate predictive model.

The project documents a complete journey from raw data to a robust, production-ready model, including a comprehensive investigation and resolution of data leakage issues inherent in the synthetic dataset. This repository serves as a portfolio piece and a potential foundation for a conference paper.

---

## 📌 Project Status: ✅ Complete

The project has been completed through all phases: data exploration, feature engineering, modeling, hyperparameter tuning, and final evaluation.

---

## 🏆 Final Model Performance

The champion model, a `RandomForestRegressor`, demonstrated exceptional performance on the unseen hold-out test set.

| Metric | Score | Interpretation |
| :--- | :--- | :--- |
| **RMSE** (Root Mean Squared Error) | **0.0129 kW** | The model's predictions have a very low typical error magnitude. |
| **MAE** (Mean Absolute Error) | **0.0107 kW** | On average, the model's prediction is off by only 0.01 kW. |
| **R-squared ($R^2$)** | **0.9777** | The model successfully explains **97.8%** of the variance in charging demand. |

---

## 🧠 Model Architecture & Key Insights

The final model is a **Random Forest Regressor** with its default hyperparameters, as extensive tuning confirmed these were optimal. A Random Forest is an ensemble learning method that operates by constructing a multitude of decision trees at training time and outputting the mean prediction of the individual trees.

### Key Success Factors:

1.  **Feature Engineering:** The most critical factor for the model's success was the creation of time-based features. The feature importance plot confirms that the model relied most heavily on **`demand_lag_24hr`**, **`demand_lag_1hr`**, and the cyclical **`hour_sin`/`hour_cos`** features. This proves that understanding the data's inherent patterns was crucial.
2.  **Data Leakage Debugging:** A significant portion of the project involved identifying and systematically removing "leaky" features from the synthetic dataset. This process, using feature importance and tree visualization, was essential for building a model that learned real patterns instead of "cheating."
3.  **Model Selection:** The Random Forest's ability to capture complex, non-linear relationships allowed it to significantly outperform simpler models like Linear Regression.

---

## 🛠️ Technology Stack

* **Language:** Python 3.10+
* **Core Libraries:** Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, XGBoost
* **Environment:** JupyterLab, Git

---

## 🚀 Getting Started

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```
2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    # On Windows: venv\Scripts\activate
    # On Mac/Linux: source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Launch JupyterLab to view the notebook:**
    ```bash
    jupyter lab
    ```
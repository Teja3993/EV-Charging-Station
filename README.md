# EV Charging Demand Forecast: A Time-Series ML Project



## 📖 Overview

This project is an end-to-end machine learning workflow to forecast Electric Vehicle (EV) charging demand based on a rich time-series dataset from California. The primary goal is to analyze historical data, engineer relevant features, and build predictive models to accurately estimate future demand.

This project documents a complete journey from raw data to robust model evaluation, including extensive debugging of data leakage issues found in the synthetic dataset.

---

## 📌 Project Status

* **Phase 1: Foundations & EDA** - ✅ Complete
* **Phase 2: Modeling & Evaluation** - ✅ Complete
* **Phase 3: Tuning & Deployment** - 🚀 In Progress

---

## 💡 Key Findings & Insights

* **Strong Hourly Pattern:** Exploratory Data Analysis revealed a powerful diurnal (24-hour) pattern, with demand consistently peaking in the evening. This proved to be the most significant predictor.
* **Weak Weekly Pattern:** In contrast, the day of the week showed little to no influence on the average charging demand.
* **Data Leakage Investigation:** Initial modeling with a `DecisionTreeRegressor` resulted in a perfect but impossible RMSE of 0.00. A deep-dive investigation using feature importance and tree visualization uncovered multiple "leaky" features (`Power Outages`, `Grid Stability Index`, etc.).
* **Synthetic Dataset Conclusion:** The persistent data leakage confirmed that the dataset is synthetic, with the target variable being a deterministic function of the features. This was proven by switching to a simpler `LinearRegression` model, which produced a realistic, non-zero error score.

---

## 📊 Modeling Results

After identifying and removing all leaky features, several models were trained and evaluated. The Random Forest Regressor was the clear champion, significantly outperforming the baseline.

| Model | Evaluation Method | RMSE (kW) |
| :--- | :--- | :--- |
| Linear Regression (Baseline) | Simple Train-Test Split | 0.0863 |
| XGBoost Regressor | Simple Train-Test Split | 0.0700 |
| **Random Forest Regressor** | **5-Fold Time-Series CV** | **0.0361 (Average)** |

---

## 🛠️ Technology Stack

* **Language:** Python 3.10+
* **Core Libraries:** Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, XGBoost
* **Environment:** JupyterLab, Git

---

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
    pip install -r requirements.txt
    ```
4.  **Launch JupyterLab to view the notebook:**
    ```bash
    jupyter lab
    ```

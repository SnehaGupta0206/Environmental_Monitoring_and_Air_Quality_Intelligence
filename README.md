# Environmental Monitoring & Air Quality Intelligence

An end-to-end data analytics and machine learning project analyzing air quality across Indian cities (2015–2020), covering data cleaning, exploratory analysis, time-series forecasting, and a predictive ML model — built as part of an internship/training project.

**Live Repo:** https://github.com/SnehaGupta0206/Environmental_Monitoring_and_Air_Quality_Intelligence

---

## Project Overview

Air pollution is a major public health and environmental concern in India. This project analyzes historical air quality data to:

- Understand pollution trends across cities and seasons
- Identify the key pollutants driving poor air quality
- Forecast future AQI using time-series models
- Predict AQI from pollutant readings using machine learning
- Visualize findings through maps, charts, and an interactive dashboard

---

## Dataset

**Source:** [Air Quality Data in India (Kaggle)](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india)

The dataset contains daily and hourly air quality readings from monitoring stations across India (2015–2020), including:

| Column | Description |
|---|---|
| City | City name |
| Date | Date of the reading |
| PM2.5, PM10 | Particulate matter concentrations |
| NO, NO2, NOx, NH3 | Nitrogen-based pollutants |
| CO, SO2, O3 | Carbon monoxide, sulphur dioxide, ozone |
| Benzene, Toluene, Xylene | Volatile organic compounds |
| AQI | Air Quality Index |
| AQI_Bucket | Category (Good, Satisfactory, Poor, etc.) |

> **Note:** Due to GitHub's 100MB file limit, `station_hour.csv` (219MB) is **not included** in this repo. Download it separately from the Kaggle link above if needed — it is not used by any notebook in this project.

---

## Team & Roles

| Member | Role | Responsibilities |
|---|---|---|
| **Member 1** | Team Leader / GitHub & Documentation | Project planning, repo structure, README, research report, final report, team coordination |
| **Member 2** | Data Engineer | Data loading, cleaning, missing values, duplicates, outliers, feature engineering |
| **Member 3** | Data Analyst | Exploratory data analysis, correlation, AQI distribution, seasonal analysis, business insights |
| **Member 4** | ML Engineer | Time series forecasting (Moving Average, Exponential Smoothing, ARIMA, Prophet), ML models (Random Forest, Gradient Boosting), model evaluation |
| **Member 5** | BI & Visualization | Power BI dashboard, Folium maps, GeoPandas, executive presentation |

---

## Project Structure

```
Air-Quality-Analytics/
│
├── data/
│   ├── raw/                     # Original Kaggle dataset files
│   └── cleaned/                 # Cleaned dataset (output of Member 2's work)
│
├── notebooks/
│   ├── 01_Data_Cleaning.ipynb       # Data cleaning & preprocessing
│   ├── 02_EDA.ipynb                 # Exploratory data analysis
│   ├── 03_Trend_Analysis.ipynb      # Pollution trends & seasonal patterns
│   ├── 04_Forecasting.ipynb         # Time series forecasting (Moving Avg, ETS, ARIMA, Prophet)
│   └── 05_ML_Model.ipynb            # Random Forest / Gradient Boosting AQI prediction
│
├── dashboard/                        # Flask/Streamlit app + saved model files
|   ├── City_Air_Quality_Dashboard.pbix
│   └── Executive_Air_Quality_Dashboard.pbix              
│   ├── model.pkl
│   └── model_features.pkl
│
├── reports/
│   ├── Research_Report.pdf
│   ├── Planning.pdf
│   └── Final_Report.pdf
│
├── images/                      # Saved charts, maps, and screenshots
│
├── requirements.txt
│
└── README.md
```

---

## Key Findings & Results

### Forecasting (`04_Forecasting.ipynb`)
Compared four forecasting approaches on Delhi's daily AQI:

| Model | MAE | RMSE | MAPE |
|---|---|---|---|
| Moving Average | 58.17 | 67.46 | 41.20% |
| Exponential Smoothing | 49.54 | 64.09 | 37.13% |
| **ARIMA(5,1,2)** | **35.51** | **47.47** | **23.72%** |
| Prophet | 71.15 | 81.25 | 60.97% |

**ARIMA performed best.** The test period (Apr–Jul 2020) coincided with the COVID-19 lockdown, causing atypical AQI drops that none of the models were trained to anticipate — a genuine data limitation rather than a modeling error.

### ML Prediction (`05_ML_Model.ipynb`)
Compared Random Forest and Gradient Boosting for feature-based AQI prediction:

| Model | MAE | RMSE | R² |
|---|---|---|---|
| **Random Forest** | **21.05** | **40.34** | **0.911** |
| Gradient Boosting | 21.94 | 42.10 | 0.903 |

Feature importance showed **PM2.5 and CO together account for ~87%** of the model's predictions — consistent with known AQI sub-index weighting.

---

## Tech Stack

- **Data & Analysis:** Python, Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly, Folium, GeoPandas
- **Forecasting:** Statsmodels (Exponential Smoothing, ARIMA), Prophet
- **Machine Learning:** Scikit-learn (Random Forest, Gradient Boosting)
- **Dashboard:** Flask
- **BI:** Power BI

---

## Getting Started

### 1. Clone the repository
```
git clone https://github.com/SnehaGupta0206/Environmental_Monitoring_and_Air_Quality_Intelligence.git
cd Environmental_Monitoring_and_Air_Quality_Intelligence
```

### 2. Set up a virtual environment
```
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # macOS/Linux
```

### 3. Install dependencies
```
pip install -r requirements.txt
```

### 4. Get the dataset
Download the dataset from [Kaggle](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india) and place the CSV files in `data/raw/`.

### 5. Run the notebooks in order
```
01_Data_Cleaning.ipynb   →  02_EDA.ipynb  →  03_Trend_Analysis.ipynb  →  04_Forecasting.ipynb  →  05_ML_Model.ipynb
```

Running `05_ML_Model.ipynb` regenerates `dashboard/model.pkl`, which the Flask app depends on.

### 6. Run the dashboard
```
cd dashboard
python app.py
```

---

## Reports

- **Planning.pdf** — Project scope, objectives, timeline
- **Research_Report.pdf** — Background research and methodology
- **Final_Report.pdf** — Complete findings, insights, and recommendations

---

## Acknowledgements

Dataset provided by [Rohan Rao on Kaggle](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india), sourced from India's Central Pollution Control Board (CPCB).
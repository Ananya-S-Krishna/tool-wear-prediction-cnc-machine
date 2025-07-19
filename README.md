# Tool Wear Prediction in CNC Machines

This project implements a data-driven approach for predicting tool wear in CNC machines using multi-sensor data. It leverages supervised machine learning techniques on cutting force, vibration, and acoustic emission signals to enable predictive maintenance and improve tool life.

## Objective

To develop a predictive maintenance model that can estimate the extent of tool wear in CNC machining operations using sensor-based measurements, enabling reduced unplanned downtimes and increased manufacturing efficiency.

---

## Dataset

- **Source**: Kaggle — *“Tool wear detection in CNC turning”*
- **Size**: 104,675 rows × 11 columns
- **Sensors Used**:
  - Cutting force (`force_x`, `force_y`, `force_z`)
  - Vibration (`vibration_x`, `vibration_y`, `vibration_z`)
  - Acoustic emission (`acoustic_emission_rms`)
- **Target Variable**: `tool_wear`

## Features Used

All 7 numeric sensor readings were used as input features:
- `force_x`, `force_y`, `force_z`
- `vibration_x`, `vibration_y`, `vibration_z`
- `acoustic_emission_rms`

The following columns were excluded:
- `timestamp`, `experiment_tag`, `dataset_tag` (non-numeric or not predictive)

## Workflow

### 1. Exploratory Data Analysis (EDA)
- Summary statistics, correlation matrix, outlier checks
- Sensor pattern inspection

### 2. Data Preprocessing
- Dropped irrelevant/non-numeric columns
- Feature and target separation
- Standardized feature values using `StandardScaler`

### 3. Model Training and Comparison
Evaluated multiple regression algorithms to predict tool wear:

| Model             | MAE     | RMSE    | R²       |
|------------------|---------|---------|----------|
| Linear Regression| 0.02913 | 0.03802 | 0.12064  |
| Random Forest     | 0.01435 | 0.02053 | 0.74364  |
| XGBoost           | 0.01530 | 0.02140 | 0.72141  |
| LightGBM          | 0.01552 | 0.02158 | 0.71666  |
| **CatBoost**      | **0.01461** | **0.02052** | **0.74381** ✅ |

- **Best Model**: CatBoost Regressor

### 4. Model Export
- Final CatBoost model was saved using `joblib` as: `catboost_tool_wear_model.pkl`

## Skills & Tools Used

### Mechanical Engineering Concepts
- Tool wear analysis in CNC turning
- Multi-sensor signal interpretation (force, vibration, acoustic)
- Predictive maintenance strategies

### Machine Learning
- Regression modeling
- Feature engineering
- Model evaluation (MAE, RMSE, R²)

### Tools & Libraries
- Python, NumPy, Pandas, Matplotlib, Seaborn
- Scikit-learn, XGBoost, LightGBM, CatBoost
- Google Colab (GPU runtime)
- Git & GitHub (project versioning)

## Future Work

- Real-time sensor data streaming for deployment in manufacturing setups
- Model explainability using SHAP
- Integration with a dashboard using Streamlit

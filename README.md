# Predicting Air Quality (PM2.5) Using Regression and Classification

This project provides a complete workflow to predict PM2.5 concentration and categorize air quality (AQI Category) using machine learning. It combines time-series preprocessing, feature engineering, multiple regression models, and AQI classification in a single unified notebook.

## Project Overview

The notebook performs the following:

- Handles missing PM2.5 values using time-based interpolation to preserve time continuity.
- Performs feature engineering such as lag features, rolling averages, and time index features.
- Uses a strict time-series train test split and TimeSeriesSplit to prevent data leakage.
- Builds and evaluates multiple models for:
  - Regression: Predict PM2.5 levels.
  - Classification: Predict AQI Category.
- Conducts hyperparameter tuning to improve performance.
- Saves the final model, scaler, and features for deployment.
- Provides a user input interface to make live AQI predictions.

## Dataset

- Input file: `Real_Combine.csv`
- Index: Converted to datetime and used as the time index.
- Target Variable: `PM_25`
- Additional Generated Label: `AQI_Category` (based on PM2.5 thresholds)

## Key Steps

### 1. Data Preprocessing
- Replace zero PM2.5 values with NaN.
- Interpolate missing values based on time.
- Remove remaining NaN values using backward fill.

### 2. Feature Engineering
Features include:
- Month and day of year.
- Lag and rolling mean of PM2.5 (log-transformed).
- Lagged weather variables (Temperature, Humidity, Wind Speed, Max Wind Speed).

### 3. Train Test Split
- 80 percent training and 20 percent testing with shuffle disabled to respect time order.

### 4. Model Training and Evaluation
Models Evaluated:
| Model | R² Score | RMSE | MAE |
|------|---------|------|-----|
| Random Forest | ~0.86 | ~29.5 | ~23 |
| Ridge Regression | Moderate performance |
| XGBoost | Lower performance |
| Lasso | Poor performance |

The best performing model was Random Forest.

### 5. Hyperparameter Tuning
Tuned Parameters:
```
{
max_depth: 10,
min_samples_leaf: 4,
n_estimators: 200
}
```

Final Tuned Model Performance:
- R² approximately 0.87
- RMSE approximately 28.1
- MAE approximately 22.1

### 6. Saving Final Artifacts
The following files are generated:
```
aqi_rf_model_final.joblib
aqi_scaler_final.joblib
aqi_feature_names_final.joblib
```

### 7. User Prediction Interface
The notebook includes a prompt-based input section where users can input:
- Current date
- Temperature
- Humidity
- Wind conditions
- PM2.5 values for recent days  

The model outputs:
- Predicted PM2.5 concentration
- Corresponding AQI category

## Requirements
```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
joblib
```

Install using: ```!pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib```

## How to Run

1. Place `Real_Combine.csv` in the working directory.
2. Run the notebook sequentially.
3. After training, run the final cell to input real-time data and get predictions.


## Conclusion

This project provides a complete pipeline for air quality forecasting using machine learning. It is suitable for educational, research, and practical city-level monitoring applications. The combination of regression and classification ensures interpretability along with meaningful public-friendly outputs.

# Air Quality Prediction System - Grade C Extension

## Overview
This project predicts PM2.5 air quality levels using weather data and machine learning. For Grade C, I added **lagged features** to improve the model's prediction accuracy.

## What are Lagged Features?

Lagged features use **past values** to predict future values. In this project, I added:
- `pm25_lag_1`: PM2.5 value from **1 day ago**
- `pm25_lag_2`: PM2.5 value from **2 days ago**
- `pm25_lag_3`: PM2.5 value from **3 days ago**

### Why use lagged features?
Air quality has **time continuity** - if the air was polluted yesterday, it's likely still polluted today. By including past values, the model can learn these patterns.

## Model Comparison

I trained two models to compare the results:

| Model | Features | MSE | R² Score |
|-------|----------|-----|----------|
| **Model v1** | Weather only (no lag) | 136.20 | -0.37 |
| **Model v2** | Weather + lag features | 54.86 | 0.46 |

### Performance Improvement
- **MSE decreased by 59.7%** (lower is better)
- **R² improved from -0.37 to 0.46** (higher is better)

### What does this mean?
- **Model v1** performed worse than just guessing the average (R² is negative)
- **Model v2** can explain 46% of the variation in air quality
- Adding lagged features made the model **much more useful**

## Why did this happen?

1. **Time dependency**: Air quality doesn't change randomly - it follows patterns
2. **Weather lag**: Weather changes take time to affect air quality
3. **Pollution accumulation**: Pollutants build up over multiple days

The model learned that yesterday's air quality is a strong predictor of today's air quality.

## Implementation Details

### Step 1: Create Lagged Features
```python
# Group by city and street, then shift values
df['pm25_lag_1'] = df.groupby(['city', 'street'])['pm25'].shift(1)
df['pm25_lag_2'] = df.groupby(['city', 'street'])['pm25'].shift(2)
df['pm25_lag_3'] = df.groupby(['city', 'street'])['pm25'].shift(3)

# Remove rows with missing values (first 3 days)
df = df.dropna()
```

### Step 2: Train Both Models
- **Model v1**: Uses only weather features (temperature, wind, precipitation)
- **Model v2**: Uses weather features + 3 lagged features

### Step 3: Compare Results
Both models were trained on the same data and tested on the same period to ensure a fair comparison.

## Conclusion

Adding lagged features significantly improved the model:
- Lower error (MSE reduced by 60%)
- Better predictions (R² increased from negative to positive)
- More practical for real-world use

This shows that **historical data is important** for predicting air quality.

## Files
- `1_air_quality_feature_backfill.ipynb`: Creates features with lags
- `comapre.ipynb`: Trains and compares both models

# Neu_ISA444_Hotel_Demand_Forecast

## Project Overview

In this project, we are producing forecasts for daily hotel r=oom demand for 17 different properties. The overall goal of this project is to compare different types of forecasting models (Baseline, Statistical, Machine Learning, Neural, and Foundational) in a single, consistent workflow. With the forecast horizon being 28 days, the last 28 days for each hotel were held out to be the test set. ALl other dates before that were used for training data. 

## Models Used

- Naive (Baseline)
- Seasonal Naive (Baseline)
- AutoETS (Statistical)
- AutoARIMA (Statistical)
- LightGBM (Machine Learning) 
- AutoNBEATS (Neural)
- AutoNHITS (Neural)
- Chronos (Foundational)

## Metrics used for Evaluation

- ME (Mean Error) 
- MAE (Mean Absolute Error)
- RMSE (Root Mean Square Error)
- MAPE (Mean Absolute Percentage Error)

## Files in this Repository

- `Final_Project.ipynb` — full notebook with code and workflow
- `cv_evaluation_results.csv` — cross-validation evaluation results
- `model_win_counts.csv` — model win counts by metric
- `final_test_all_models.csv` — final test forecasts for all models
- `final_test_all_models_evaluation.csv` — final test evaluation metrics

## Model Interpretations

### Naive Model
Surprisingly, the naive model worked well. Due to the model predicting demand to stay equal to the most recent actual value, its forecast line appears flat in the plots. Its performance suggests that many hotel series had a consistently stable short term demand, where the most recent value was a useful predictor of the next 28 days.

### Seasonal Naive Model
This model repeats the weekly pattern. Based on the evaluation metrics of this model, we can see that there are more applicable models to create better predictions. This suggests that the weekly seasonality alone was not enough to eexplain the demand patterns and variation within the hotel dataset.

### AutoETS
This model is able to capture the trend and seasonal patterns using exponential smoothing. While is performed decently, especially for the hotels with less irregular spikes in demand. Even with that being said, it is not the strongest overall model. This means that the smoothing did not always capture the sudden changes within the dataset.

### AutoARIMA
AutoARIMA is one of the strongest scored models. The reason it performed well is due to the fact that it can capture trend, autocorrelation, and repeating patterns within the dataset. With a strong RMSE, we can see that it handled forecasting errors much better than some of the other models.

### LightGBM
LightGBM also perfromed very strong, especially for the MAE metric. This tells us that it was good at reducing forecast errors across the different hotels. This particular model uses lags and rolling averages. This allows the model to interpret and learn different patterns from the recent demand history. With its performance, it is able to show that machine learning features helped for some of the hotels.

### AutoNBEATS
In comparison to the more simple models, this model had limited wins. This may be due to the fact that the dataset was small, and neural models often perform better on more data. However, it still provided useful comparison value.

### AutoNHITS
This was one of the worst performing models. It did not win very often across some of the different metrics used for evaluation. This shows that it may have not fit the small dataset as well as the models that are more simple. While it scored the best on the bias metric, it still is not very accurate because the bias metric only tells us if it it likely the model will over or under predict. 

### Chronos
This model performed well for some hotels, especially under the RMSE metric. This tells us that foundation models can produce good forecasts without being heavily customized. However, Chronos did not clearly dominate the other models as some others did. This shows that foundation models are not always better than traditional or simple approaches.

### Overall Interpretation
Overall, the strongest models were Naive, LightGBM, AutoARIMA, and Chronos. Naive performed well because short-term hotel demand was often stable. LightGBM performed well because the lags and rolling average helped capture recent patterns in the hotel demand. AutoARIMA and Chronos were also competitive, especially for RMSE.

## Forecast Plots

Forecast vs. actual plots were created for each hotel series using the best performing models. These plots compare actual hotel demand from the 28-day test period against model predictions.

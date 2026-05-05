# Predicting Hospital Length of Stay Using LightGBM with Explainable AI
Built a LightGBM regression model with Optuna tuning, achieving ~85% MAE reduction (1.9 → 0.29), validated via shuffled-target testing and interpreted using SHAP to identify key clinical and behavioral drivers.

## Key Observations
1. Model Choice (LightGBM)
- Selected LightGBM for its strength on tabular data with mixed feature types.
- Tree-based models effectively capture non-linear relationships and are robust to noise and feature interactions.
2. Hyperparameter Optimization
- Used Optuna for efficient hyperparameter tuning.
- Achieved better performance compared to manual/grid search by exploring the parameter space intelligently.
3. Multicollinearity
- High multicollinearity observed among some clinical features (e.g., sodium, BMI, respiration).
- Did not significantly impact performance since tree-based models are less sensitive to correlated inputs.
4. Model Performance
- Achieved MAE ≈ 0.29 compared to baseline ≈ 1.9 (~85% improvement).
- Approximately 97% of predictions are within ±1 day, indicating strong predictive accuracy.
5. Data Characteristics
- Target variable (length of stay) exhibits low noise and a concentrated distribution (primarily 2–6 days).
- Length of stay is deterministically derived from admission and discharge timestamps, resulting in highly consistent labels.
- This makes the prediction task more structured and predictable compared to real-world hospital data, where variability arises from clinical uncertainty, operational constraints, and human decision-making.
6. Model Validation
- Performed a shuffled-target test to validate model integrity.
- MAE increased to ~1.94 (≈ baseline), confirming the model is learning meaningful patterns and not leaking information.
7. Feature Insights (from SHAP)
- Key drivers include:
``bash
rcount (patient visit frequency)
facid (institutional effect)
Clinical indicators (glucose, creatinine, hematocrit)
Indicates both patient history and hospital factors influence length of stay.
``

## Limitations & Future Work
1. Dataset is highly structured and clean with deterministic target → easier than real-world scenarios
2. Model struggles on rare long-stay cases (>10 days)
3. Future work:
- classification-based framing (short/medium/long stay)
- handling class imbalance
- external dataset validation

- **Dataset** : [https://www.kaggle.com/datasets/aayushchou/hospital-length-of-stay-dataset-microsoft/data]url
- **Notebook** : [https://www.kaggle.com/code/shravyadsouza22/predicting-hospital-length-of-stay-using-lightgbm]url

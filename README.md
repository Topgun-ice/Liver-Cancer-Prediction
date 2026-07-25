# Liver Cancer Prediction (Logistic Regression)

### Medical Disclaimer
This project is for educational purposes only. It is not a medical device, and its predictions
should not be used for real clinical decisions. The model has not been validated on external
datasets, and no regulatory approvals have been obtained.

## Overview
Logistic regression model predicting liver cancer risk from clinical features (AST, ALT, age, gender). Includes EDA, feature scaling, model evaluation (accuracy, precision, recall, ROC-AUC), and coefficient-based feature importance analysis.

## Dataset
- Source: liver_cancer_dataset/kaggle.com
- Target variable: `has_liver_cancer` (binary)
- Note: raw data is not included in this repo — see `data/` for details on obtaining it.

## Approach
1. Data loading and inspection (missing values, data types)
2. Data preprocessing (encoding categorical variables, feature scaling)
3. Exploratory Data Analysis (class balance, correlation heatmap)
4. Model training (Logistic Regression, 80/20 stratified train-test split)
5. Model evaluation (accuracy, precision, recall, F1, confusion matrix, ROC-AUC)
6. Feature importance interpretation (scaled coefficients)
7. Model persistence (saved to `models/`)

## Results
The logistic regression model was trained on an 80/20 stratified train-test split (n = 4000),
with 97.425% of samples labeled as having liver cancer.

| Metric    | Score |
|-----------|-------|
| Accuracy  | 0.975 |
| Precision | 0.969 |
| Recall    | 1.000 |
| F1-score  | 0.995 |
| ROC-AUC   | 0.829 |

### Interpretation
- Accuracy of 0.975 indicates the model correctly classified 100% of test cases overall.
  [If classes are imbalanced, add: However, given the class imbalance (only 97.425% positive
  cases), accuracy alone is not a fully reliable metric — precision, recall, and ROC-AUC below give
  a more complete picture.]

- Precision of 0.969 means that when the model predicted a positive case (liver cancer), it was
  correct 96.9% of the time.

- Recall of 1.000 means the model correctly identified 100% of all actual positive cases. In a
  medical screening context, recall is often the more critical metric, since missing a true positive
  (a false negative) carries a higher cost than a false alarm.

- ROC-AUC of 0.829 reflects the model's ability to distinguish between the two classes across all
  classification thresholds, where 1.0 is perfect separation and 0.5 is no better than random guessing.

### Feature Importance

The top features influencing the model's predictions (based on scaled logistic regression coefficients)
were:

| Feature   | Coefficient | Direction                  |
|-----------|-------------|----------------------------|
| edema     | 0.679245    | ↑ increases predicted risk |
| ast       | 0.613466    | ↑ increases predicted risk |
| platelets | -0.474857   | ↓ decreases predicted risk |

A positive coefficient indicates the feature is associated with a higher predicted likelihood of liver
cancer in this dataset; a negative coefficient indicates the opposite. These associations reflect
patterns in the training data only and should not be interpreted as causal relationships.

### Limitations

- The model has not been validated on external or held-out datasets beyond the single train-test split.
- [Add any known limitations: dataset size, missing features, potential sampling bias, etc.]
- As noted in the disclaimer above, this model is not intended for real clinical use.

## Project Structure
```
liver-cancer-prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── liver_cancer_dataset.csv   
├── notebooks/
│   └── project-4.ipynb
└── models/
    ├── logistic_model.pkl
    └── scaler.pkl
│
└── results/
    └── (optional: confusion matrix.png / ROC Curve.png)    
```

## How to Run
```bash
pip install -r requirements.txt
jupyter notebook notebooks/Liver Cancer Prediction (Logistic Regression).ipynb
```

## License
MIT

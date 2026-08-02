# Spotter.ai Machine Learning Engineer Assessment
## Freight Rate Prediction

## Project Overview

This repository contains my solution for the Spotter.ai Machine Learning Engineer Assessment.

The objective of this assessment is to build a machine learning pipeline capable of predicting freight load rates using historical shipment data. The solution includes data exploration, preprocessing, feature engineering, model development, validation, and prediction generation for unseen freight loads.

The final solution uses CatBoost Regressor as the primary prediction model after comparing its performance against a Linear Regression baseline.

---

## Repository Structure

```
spotter-freight-rate-prediction/
│
├── Freight_Rate_Prediction.ipynb
│  
│
├── outputs/
│   ├── validation_predictions.csv
│   └── december_chart_predictions.csv
│
├── score_result/
│   └── candidate_december.png
│
├── requirements.txt
├── score.py
├── README.md
└── .gitignore
```

---

## Dataset

The assessment provides three datasets:

- **train_test.csv** – Historical labelled freight loads used for model development.
- **validation.csv** – Unseen freight loads requiring final predictions.
- **december_chart_inputs.csv** – Fixed December loads used to generate the required prediction chart.

> **Note:** The datasets provided as part of the Spotter.ai assessment are not included in this public repository.

---

## Project Workflow

The complete workflow consists of the following stages:

1. Data Exploration
2. Data Cleaning
3. Missing Value Handling
4. Feature Engineering
5. Train/Validation Split
6. Baseline Model (Linear Regression)
7. CatBoost Model Development
8. Model Evaluation
9. Final Validation Predictions
10. December Prediction Generation
11. Output Validation using `score.py`

---

## Exploratory Data Analysis

The following analyses were performed:

- Dataset inspection
- Missing value analysis
- Duplicate detection
- Distribution of target variable
- Correlation analysis
- Relationship between shipment distance and freight rate
- Equipment type analysis

---

## Feature Engineering

The following features were created to improve model performance:

### Date Features

- Year
- Month
- Day
- Day of Week
- Week of Year
- Quarter
- Weekend Indicator

### Route Features

- Route (Pickup → Delivery)

### Distance Features

- Distance Bucket
- Weight per Mile

### Frequency Encoding

- Pickup Frequency
- Delivery Frequency
- Route Frequency
- Equipment Frequency

---

## Model Development

Two models were evaluated.

| Model | MAE | RMSE | R² |
|------|------:|------:|------:|
| Linear Regression | 144.09 | 652.66 | 0.818 |
| CatBoost Regressor | 136.96 | 649.89 | 0.819 |

CatBoost was selected as the final model due to its superior predictive performance and its ability to naturally handle categorical variables.

---

## Validation Strategy

- The development dataset was split into Training and Validation sets using an 80/20 split.
- Model performance was evaluated using:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
  - R² Score
- After model selection, CatBoost was retrained on the complete labeled dataset to generate predictions for the provided validation set.
- A second CatBoost model was trained using the subset of features available in the December dataset to ensure consistency between training and inference.

---

## Outputs

The repository generates:

- `validation_predictions.csv`
- `december_chart_predictions.csv`
- `candidate_december.png`

The provided `score.py` script is used to validate the generated prediction files.

---

## Installation

Clone the repository

```bash
git clone <repository-url>
cd spotter-freight-rate-prediction
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

## Run Instructions

Open and execute:

```
notebooks/Freight_Rate_Prediction.ipynb
```

After generating the prediction files, validate them using:

```bash
python score.py \
--predictions outputs/validation_predictions.csv \
--december-predictions outputs/december_chart_predictions.csv
```

The validation script generates:

```
scorer_results/candidate_december.png
```

---

## Author

**Mohammed Dhayan Ahmed**

Machine Learning Engineer Assessment Submission

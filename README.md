# Customer Churn Prediction Using Logistic Regression

## Project Overview

This project aims to predict customer churn — whether a customer will leave the service — using logistic regression on a telecom dataset. The goal is to analyze how different feature selections affect the model's predictive performance, measured by log loss and confusion matrix metrics.

---

## Dataset Description

The dataset contains 200 samples with the following features:

| Feature   | Description                          |
|-----------|------------------------------------|
| tenure    | Number of months the customer stayed|
| age       | Customer's age                     |
| address   | Customer's address      |
| income    | Customer's income                  |
| ed        | Education level                    |
| employ    | Employment duration                |
| equip     | Number of equipment owned          |
| callcard  | Whether customer uses call card  |
| wireless  | Whether customer uses wireless   |
| churn     | Target variable: 1 if churned, 0 otherwise |

---

## Data Preprocessing

- Loaded data from CSV file.
- Selected subsets of features based on experiments.
- Converted target variable `churn` to integer type.
- Standardized features using `StandardScaler` for normalization.
- Split data into training (80%) and testing (20%) sets with fixed random seed (`random_state=4`) for reproducibility.

---

## Experiments and Feature Selection

Several experiments were performed by modifying input features and observing changes in model performance:

| Experiment                                        | Features Included                              | Log Loss    |
|-------------------------------------------------|-----------------------------------------------|-------------|
| Base Model                                       | tenure, age, address, income, ed, employ, equip | 0.6258      |
| Adding `callcard` feature                         | Base + callcard                               | 0.6039      |
| Adding `wireless` feature                         | Base + wireless                               | 0.7227      |
| Adding both `callcard` and `wireless`            | Base + callcard + wireless                    | 0.7761      |
| Removing `equip` feature                          | All except `equip`                            | 0.5302      |
| Removing `income` and `employ` features          | Base minus income & employ                     | 0.6529      |
| Removing `equip` + balanced class weights (class_weight='balanced') | Base minus equip + balanced classes         | 0.4648      |

---

## Model Training

- Logistic Regression model trained on normalized feature sets.
- `class_weight='balanced'` used in final experiment to handle class imbalance.
- Model evaluated on test set using log loss and confusion matrix.

---

## Results

- The lowest log loss (best model) was obtained after **removing the `equip` feature and balancing class weights**.
- Confusion matrix and classification metrics confirmed improved recall and precision for minority class (churned customers).
- Adding `callcard` improved the base model slightly, while adding `wireless` did not help and even worsened performance.
- Removing `income` and `employ` features slightly reduced performance compared to base.

---

## Model Evaluation Metrics

Example confusion matrix from best model (after removing `equip` and balancing classes):

[[22 3]
[ 6 9]]


Interpretation:

- True Negatives (TN): 22 customers correctly predicted as not churned.
- False Positives (FP): 3 customers wrongly predicted as churned.
- False Negatives (FN): 6 customers wrongly predicted as not churned.
- True Positives (TP): 9 customers correctly predicted as churned.

---

## Visualizations

- Bar plots of feature coefficients from logistic regression show which features have the strongest positive or negative impact on churn prediction.
- Confusion matrices visually represent prediction accuracy and error types.

---

## How to Run

1. Clone the repo:
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>



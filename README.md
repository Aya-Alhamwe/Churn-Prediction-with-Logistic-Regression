# 📊 Customer Churn Prediction Using Logistic Regression

## 📁 Project Overview

This project aims to predict customer churn — whether a customer will leave the service — using logistic regression on a telecom dataset. The goal is to analyze how different feature selections affect the model's predictive performance, measured by **log loss** and **confusion matrix** metrics.

---

## 📂 Dataset Description

The dataset contains 200 samples with the following features:

| 🧩 Feature   | 📝 Description                          |
|-------------|-----------------------------------------|
| `tenure`    | Number of months the customer stayed    |
| `age`       | Customer's age                          |
| `address`   | Customer's address                      |
| `income`    | Customer's income                       |
| `ed`        | Education level                         |
| `employ`    | Employment duration                     |
| `equip`     | Number of equipment owned               |
| `callcard`  | Whether customer uses call card         |
| `wireless`  | Whether customer uses wireless          |
| `churn`     | 🎯 Target variable: 1 if churned, 0 otherwise |

---

## 🧼 Data Preprocessing

- ✅ Loaded data from CSV file.
- ✅ Selected subsets of features based on experiments.
- ✅ Converted target variable `churn` to integer type.
- ✅ Standardized features using `StandardScaler` for normalization.
- ✅ Split data into training (80%) and testing (20%) sets with fixed `random_state=4` for reproducibility.

---

## 🧪 Experiments and Feature Selection

Several experiments were performed by modifying input features and observing changes in model performance:

| 🔬 Experiment                                       | ✅ Features Included                              | 📉 Log Loss    |
|----------------------------------------------------|--------------------------------------------------|----------------|
| Base Model                                         | `tenure, age, address, income, ed, employ, equip`| **0.6258**     |
| Adding `callcard` feature                          | Base + `callcard`                                | 0.6039         |
| Adding `wireless` feature                          | Base + `wireless`                                | 0.7227         |
| Adding both `callcard` and `wireless`              | Base + `callcard`, `wireless`                    | 0.7761         |
| Removing `equip` feature                           | All except `equip`                               | 0.5302         |
| Removing `income` and `employ`                     | Base minus `income`, `employ`                    | 0.6529         |
| Removing `equip` + balanced class weights ⚖️       | No `equip`, with `class_weight='balanced'`       | 🥇 **0.4648**   |

---

## 🧠 Model Training

- Trained logistic regression on normalized features.
- Used `class_weight='balanced'` in the final experiment to handle **class imbalance**.
- Evaluated using **log loss** and **confusion matrix** on the test set.

---

## ✅ Results

- ⭐ **Best result:** Removing `equip` + using `class_weight='balanced'` led to lowest log loss.
- 📉 **Adding `wireless`** worsened performance.
- 💡 Removing `income` and `employ` slightly reduced performance vs. base.
- 📈 **Improved precision and recall** for churn class using balanced weighting.

---

## 📊 Model Evaluation Metrics

**Confusion matrix (best model):**

[[22 3]
[ 6 9]]


---

## 🚀 How to Run

1. Clone the repo.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt

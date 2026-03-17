# Instacart Market Basket Analysis
## Predicting Product Reorders with Machine Learning

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3+-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-1.7+-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## Overview

This project builds an **end-to-end machine learning pipeline** to predict whether a customer will reorder a product in their next Instacart purchase. The problem mirrors real-world e-commerce challenges faced by companies like Amazon, iFood, and Rappi.

**Business goal:** Power a personalized recommendation engine that increases basket size and customer retention.

---

## Dataset

[Instacart Market Basket Analysis — Kaggle](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)

| File | Description | Rows |
|---|---|---|
| `orders.csv` | One row per order | 3.4M |
| `order_products__prior.csv` | Products in each order | 32M |
| `products.csv` | Product catalog | 49K |
| `aisles.csv` | Aisle reference | 134 |
| `departments.csv` | Department reference | 21 |

---

## Project Structure
```
instacart-reorder-prediction/
│
├── instacart_analysis.ipynb   # Main notebook (full pipeline)
└── README.md
```

---

## Methodology

### 1. Exploratory Data Analysis
- Overall reorder rate: **41%**
- Peak shopping hour: **10am**
- Busiest day: **Sunday**
- Median days between orders: **7 days**
- Dairy eggs and beverages have the highest reorder rates (~65%+)

### 2. Feature Engineering
Three groups of features were created:

| Group | Features | Rationale |
|---|---|---|
| User × Product | `up_times_ordered`, `up_reorder_rate`, `up_order_span`, `up_orders_since_last` | Captures individual habits per product |
| Product | `product_reorder_rate`, `product_total_orders`, `product_popularity` | Measures inherent reorderability |
| User | `user_avg_days_between`, `user_regularity`, `user_std_days_between` | Captures shopping schedule patterns |

### 3. Modeling
Three models were trained and compared:

| Model | ROC-AUC |
|---|---|
| Logistic Regression | 0.9039 |
| Random Forest | 0.9039 |
| **XGBoost** | **0.9038** |

> All three models achieved nearly identical AUC (~0.90), indicating that **feature engineering is the primary driver of performance** — a hallmark of well-structured data science work.

### 4. Best Model Performance (XGBoost)
- **Accuracy:** 84%
- **Precision (Reorder):** 0.84
- **Recall (Reorder):** 0.88
- **F1-score (Reorder):** 0.86

### 5. Recommendation System
A function `recommend_products(user_id, top_n)` returns the top N products most likely to be reordered by a given user, ranked by predicted probability.

---

## 💡 Key Insights

1. **Past behavior dominates** — `up_times_ordered` and `up_reorder_rate` are the strongest predictors. The model improves significantly as users build purchase history.
2. **Recency matters** — users with long gaps since their last purchase of a product are much less likely to reorder it.
3. **Weekly shoppers dominate** — with a median of 7 days between orders, recommendations should be timed around weekly shopping cycles.
4. **Product type drives reorderability** — staple categories like dairy and beverages reorder at ~65%+, making them ideal for auto-replenishment features.

---

## Tech Stack

- **Python 3.10+**
- **Pandas** — data manipulation and feature engineering
- **Scikit-learn** — Logistic Regression, Random Forest, model evaluation
- **XGBoost** — gradient boosting model
- **Matplotlib / Seaborn** — visualizations

---

## How to Run

**On Kaggle (recommended):**
1. Open the notebook directly on Kaggle
2. The dataset is already linked — just click **Run All**

**Locally:**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
jupyter notebook instacart_analysis.ipynb
```

---

## Author

**Alessandra Gonçalves**  
Data Science Student @ CEUB  
[LinkedIn](https://www.linkedin.com/in/alessandra-souza-gonçalves-271750269) • [GitHub](https://github.com/alessandrasgoncalves23)

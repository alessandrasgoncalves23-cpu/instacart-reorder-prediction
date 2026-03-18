# Instacart Market Basket Analysis  
## Predicting Product Reorders for Personalized Recommendations

---

## Overview

This project builds an end-to-end machine learning pipeline to predict whether a customer will reorder a product in their next purchase.

The problem reflects real-world challenges in e-commerce platforms such as Amazon, iFood, and Rappi, where understanding customer behavior is essential to drive retention and increase revenue.

The core objective is to support a recommendation system capable of suggesting products that users are most likely to purchase again.

---

## Business Problem

E-commerce companies rely heavily on repeat purchases to sustain growth. However, predicting which products a customer will reorder is a complex task due to variability in behavior, product types, and purchase frequency.

Accurate reorder prediction enables:

- Personalized product recommendations
- Increased average order value
- Improved customer retention
- Better inventory planning and demand forecasting

---

## Dataset

Instacart Market Basket Analysis Dataset (Kaggle)

| File | Description | Rows |
|---|---|---|
| `orders.csv` | One row per order | 3.4M |
| `order_products__prior.csv` | Products per order | 32M |
| `products.csv` | Product catalog | 49K |
| `aisles.csv` | Aisle metadata | 134 |
| `departments.csv` | Department metadata | 21 |

The dataset contains transactional data linking users, products, and purchase behavior over time.

---

## Project Structure

instacart-reorder-prediction/
│
├── instacart_analysis.ipynb   # End-to-end pipeline
└── README.md
---

## Methodology

### 1. Exploratory Data Analysis

Initial analysis revealed key behavioral patterns:

- Overall reorder rate: 41%
- Peak shopping hour: 10 AM
- Busiest day of the week: Sunday
- Median time between orders: 7 days
- High reorder rates in staple categories such as dairy and beverages (~65%+)

---

### 2. Feature Engineering

Feature engineering was the most critical component of the project. Three main groups of features were created:

**User-Product Interaction Features**
- up_times_ordered
- up_reorder_rate
- up_order_span
- up_orders_since_last

These features capture how each individual user interacts with specific products.

**Product-Level Features**
- product_reorder_rate
- product_total_orders
- product_popularity

These measure the inherent likelihood of a product being reordered.

**User-Level Features**
- user_avg_days_between
- user_regularity
- user_std_days_between

These capture user purchasing patterns and consistency over time.

---

### 3. Modeling

Three models were trained and evaluated:

| Model | ROC-AUC |
|---|---|
| Logistic Regression | 0.9039 |
| Random Forest | 0.9039 |
| XGBoost | 0.9038 |

All models achieved similar performance, indicating that feature engineering was the primary driver of predictive power.

---

### 4. Model Performance

Best model: XGBoost

- Accuracy: 84%
- Precision (Reorder): 0.84
- Recall (Reorder): 0.88
- F1-score (Reorder): 0.86
- ROC-AUC: ~0.90

These results demonstrate strong predictive capability for identifying reorder behavior.

---

### 5. Recommendation System

A recommendation function was implemented:

recommend_products(user_id, top_n) 
This function returns the top N products most likely to be reordered by a given user, ranked by predicted probability.

---

## Key Insights

- Past behavior is the strongest predictor of future purchases. Features such as reorder frequency and purchase history dominate model performance.
- Recency plays a significant role. The longer the time since the last purchase, the lower the probability of reorder.
- Most users follow a weekly shopping cycle, with a median of 7 days between purchases.
- Essential product categories such as dairy and beverages exhibit significantly higher reorder rates, making them ideal for automated replenishment strategies.

---

## Business Impact

This solution can be applied in real-world systems to:

- Increase conversion rates through personalized recommendations
- Improve customer retention by anticipating repeat purchases
- Optimize inventory management with better demand predictions
- Increase average basket size through targeted product suggestions

Even small improvements in reorder prediction accuracy can translate into substantial revenue gains at scale.

---

## Production Considerations

To move this solution into a production environment:

- Deploy the model as a REST API for real-time recommendations
- Schedule batch predictions for active users on a daily or weekly basis
- Automate the feature engineering pipeline using tools such as Airflow
- Implement continuous retraining as new data becomes available
- Monitor model performance and drift over time

---

## Tech Stack

- Python 3.10+
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn

---

## How to Run

### Kaggle (Recommended)

1. Open the notebook on Kaggle
2. Run all cells (dataset is already linked)

--

## Future Improvements

- Incorporate deep learning models for sequential behavior (RNNs, Transformers)
- Build a collaborative filtering recommendation system
- Implement real-time recommendation pipelines
- Optimize model performance with hyperparameter tuning
- Expand feature set with temporal and behavioral signals

---

## Author

Alessandra Gonçalves  
Data Science Student  

LinkedIn: https://www.linkedin.com/in/alessandra-souza-gonçalves-271750269  
GitHub: https://github.com/alessandrasgoncalves23  

---


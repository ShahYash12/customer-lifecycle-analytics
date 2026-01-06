# 📊 Customer Growth Intelligence Platform  
**End-to-End Data Science & Analytics Project**

---

## 🔍 Project Overview

This project builds an **end-to-end Customer Growth Intelligence platform** that combines **analytics, data engineering, and machine learning** to understand, predict, and optimize customer behavior.

Rather than treating churn, LTV, and product recommendations as isolated problems, this project integrates them into a **single customer-centric modeling pipeline** using real transactional data augmented with realistic repeat-purchase behavior.

The outcome is a **production-style system** that enables:
- Customer churn prediction
- Customer lifetime value (LTV) forecasting
- Next-category purchase prediction
- Customer segmentation
- Sales and revenue analytics
- ROI-style decision support (e.g., return on CAC)

---

## 🎯 Business Objectives

The platform answers key business questions such as:

- Which customers are most likely to churn in the next 90 days?
- What is the expected future value of each customer?
- Which product category is a customer most likely to purchase next?
- How should customers be segmented for retention and growth?
- Where is future revenue at risk?
- How can marketing spend be optimized using predicted LTV vs CAC?

---

## 🧱 Data Sources

The project is based on the **Olist e-commerce dataset**, which includes:
- Customers
- Orders
- Products
- Categories
- Payments
- Reviews
- Geolocation

Since the original dataset contains mostly **single-purchase customers**, the data was **carefully augmented with synthetic repeat purchases** while preserving:
- Category-level buying patterns
- Order value distributions
- Time gaps between purchases
- Realistic customer behavior

This ensures modeling realism without introducing data leakage.

---

## 🏗️ Data Architecture (Warehouse → Modeling)

The project follows a **modern analytics architecture**:

### 1️⃣ Data Warehouse Layer
- `dim_customers.csv`
- `fact_orders.csv`
- `customer_order_aggregates.csv`

These tables represent the **source of truth** and mirror how real companies structure analytical databases.

---

### 2️⃣ Feature Engineering & Rolling Snapshots

To enable **time-aware modeling**, the project uses **30-day rolling customer snapshots**.

Each snapshot represents:

> “What we knew about a customer at that point in time.”

Key engineered features include:
- Recency, frequency, and monetary metrics (RFM)
- Orders and revenue in last 30 / 60 / 90 days
- Days since last purchase
- Average time between purchases
- Basket volatility
- Category diversity
- Customer density (city & state)
- Age buckets

Snapshots ensure:
- No data leakage  
- Realistic train/test splits  
- Production-style scoring capability  

---

## 🤖 Machine Learning Models & Results

### 1️⃣ Churn Prediction (Binary Classification)

**Objective:**  
Predict whether a customer will churn in the next **90 days**.

**Models Used:**
- Logistic Regression (baseline, interpretable)
- Gradient Boosting (XGBoost)

**Evaluation Strategy:**
- Temporal train/test split
- ROC-AUC as the primary metric
- Business validation via churn lift and revenue-at-risk analysis

**Performance:**
- **ROC-AUC:** ~0.72–0.78  
- **High-risk segment churn rate:** 2–3× higher than baseline  
- Strong monotonic relationship between predicted risk and actual churn

**Outputs:**
- `predicted_churn_prob`
- Churn risk segment: Low / Medium / High

**Business Impact:**
- Enables targeted retention campaigns
- Quantifies revenue at risk
- Supports prioritization of high-value, high-risk customers

---

### 2️⃣ Next Purchase Category Prediction (Multiclass Recommendation)

**Objective:**  
Predict the **next product category** a customer is most likely to purchase.

**Key Challenges:**
- High-cardinality target space (~70+ categories)
- Sparse and non-loyal purchasing behavior
- Sequence-dependent nature of category transitions

**Model Used:**
- Multiclass Gradient Boosting (XGBoost)

**Evaluation Approach:**
- Focused on **Top-K accuracy** instead of Top-1 accuracy  
- This aligns with real-world recommendation systems

**Performance:**
- **Top-1 Accuracy:** ~25-32%  
- **Top-3 Accuracy:** ~37-45%  
- Significantly higher than random baseline for a 70+ class problem

**Outputs:**
- Top-3 recommended categories per customer snapshot

**Business Impact:**
- Supports personalized merchandising
- Enables cross-sell and upsell strategies
- More realistic than forcing a single-category prediction

---

### 3️⃣ Customer Lifetime Value (LTV) Forecasting

**Objective:**  
Predict customer **future monetary value** over a 1-year and 2-year horizon.

**Key Data Characteristics:**
- Highly skewed LTV distribution
- Over 50% of customers have zero future spend
- Long-tail high-value customers

**Models Used:**
- Ridge Regression (baseline)
- Gradient Boosting Regression

**Evaluation Metrics:**
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

**Observed Performance (Raw LTV):**
- **MAE:** ~50  
- **RMSE:** ~57 

Given:
- Median LTV = 225  
- Mean LTV ≈ 350  
- Heavy-tailed distribution  

These results are **expected and realistic** for raw LTV modeling.

**Outputs:**
- Predicted LTV (365 days)
- Predicted spend horizons (1–2 years)

**Business Impact:**
- Customer prioritization by long-term value
- Marketing ROI estimation (LTV vs CAC)
- Budget allocation for retention and acquisition

---

## 📊 Customer Segmentation

Customers are segmented using:
- Churn risk
- Predicted LTV
- Purchase frequency
- Category diversity
- Spending volatility

This enables actionable segments such as:
- High-value / high-risk customers
- Low-value / low-risk customers
- Growth-potential customers

---

## 📈 Analytics & BI Enablement

All model outputs are consolidated into a **customer scoring mart**, designed for BI tools such as **Tableau or Power BI**.

Example dashboards include:
- Churn risk distribution
- Revenue at risk
- Predicted LTV by segment
- Category recommendation heatmaps
- Customer prioritization tables

---

## 🧠 Why This Project Is Different

This is **not a single-model notebook project**.

What makes it strong:
- End-to-end pipeline (data → features → ML → BI)
- Time-aware snapshot modeling (no leakage)
- Multiple ML problems solved on the same dataset
- Strong business framing (ROI, CAC, revenue risk)
- Realistic data augmentation
- Industry-style architecture

---

## 🚀 Skills Demonstrated

- Data modeling & analytics engineering
- Feature engineering for temporal customer data
- Classification & regression modeling
- Handling imbalanced and zero-inflated targets
- Model evaluation beyond accuracy
- Translating ML outputs into business decisions

---

## 📌 Interview-Ready Summary

> “I built an end-to-end customer growth intelligence platform where I engineered leakage-safe rolling snapshots, trained churn, LTV, and recommendation models, and connected model outputs to BI dashboards to support retention, personalization, and marketing ROI decisions.”

---

## 📂 Repository Structure

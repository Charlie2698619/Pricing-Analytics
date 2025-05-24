# Pricing-Analytics

# 🛍️ Customer Segmentation & Uplift Modeling for Retail Promotion Strategy

## 📌 Project Overview

This project leverages historical retail transaction data to identify customer segments and evaluate the impact of promotional discounts on sales. By combining unsupervised learning (KMeans clustering) with rule-based personas and uplift modeling, we generate insights to optimize targeting, timing, and discount strategy for personalized marketing.

---

## 🧠 Objectives

- Segment customers based on transactional behavior and demographics
- Estimate price elasticity for each segment and product category
- Evaluate uplift in revenue from promotional discounts
- Present findings through an interactive Power BI dashboard

---

## 🗂️ Data Sources

The dataset is sourced from [Kaggle Retail Transaction Dataset](https://www.kaggle.com/datasets/fahadrehman07/retail-transaction-dataset) and includes:

- `CustomerID`, `ProductID`, `ProductCategory`
- `Quantity`, `Price`, `TotalAmount`, `DiscountApplied(%)`
- `Competitor Price`, `Seasonal Factor`, `TransactionDate`

---

## 🔍 Methodology

### 1. **Data Preparation**
- Cleaned and standardized transaction data
- One-hot encoded categorical variables
- Engineered features: `Revenue`, `Treatment`, `Elasticity`, `Uplift`

### 2. **Customer Segmentation**
- Applied KMeans clustering (k=7) on normalized behavioral features
- Labeled each customer with a `Segment`

### 3. **Rule-Based Persona Assignment**
- Defined personas using spend level, discount sensitivity, elasticity, and category preference:

Each customer was classified into a persona using the following logic:

DAX
Persona = 
SWITCH(TRUE(),
    [Avg Spend] >= 300 && [Avg Discount%] < 10 && [Avg Elasticity] > -0.2, "Loyal Spenders",
    [Avg Spend] < 150 && [Avg Discount%] >= 10 && [Avg Elasticity] < -0.4, "Bargain Hunters",
    [Avg Discount%] >= 5 && [Avg Discount%] < 15 && [Avg Elasticity] < -0.5, "Functional Deal Seekers",
    [Avg Discount%] >= 10 && [Avg Elasticity] < -0.6 && [Avg Spend] < 100, "Impulse Buyers",
    "General Shopper"
)


### 4. **Uplift Modeling**
- Two-model regression approach:
  - Model 1: Revenue for treated group (promo applied)
  - Model 2: Revenue for control group (no promo)
- Computed uplift as: `Predicted_Treated - Predicted_Control`

### 5. **Persona × Product Strategy Mapping**
- Mapped each persona to their best-performing product category
- Identified combinations with high uplift and low elasticity loss

---

## 📊 Power BI Dashboard

The final output includes a multi-page Power BI report featuring:

- 🔹 Marketing Overview
- 🔹 Sales Overview 
- 🔹 Promo Effect Overview
- 🔹 Customer Segmentation profile
- 🔹 Strategic recommendations matrix

---

## 📦 Files Included

| File                          | Description                          |
|-------------------------------|--------------------------------------|
| `retail_sales.csv`            | Cleaned retail transaction dataset   |
| `customer_profiles.csv`       | Aggregated customer-level summary    |
| `uplift_summary.csv`          | Uplift scores by segment/category    |
| `retail_uplift_ready.csv`     | Final dataset for Power BI dashboard |
| `PowerBI_Dashboard.pbix`      | Interactive report (not in repo — see release) |

---

## 🚀 Key Results

- Identified 7 distinct customer segments with unique behaviors
- Uplift modeling revealed that only 3 of 7 segments respond positively to promos
- Segment-persona matching improved campaign targeting accuracy
- Persona × Category × Season insights support a smarter promo calendar

---

## 💡 How to Use

1. Clone the repo
2. Open and explore datasets in `/data/`
3. Load `retail_uplift_ready.csv` into Power BI
4. Review visuals and filters on customer segments, personas, uplift scores
5. Use the dashboard insights to plan smarter, more profitable promotions

---

## 📬 Contact

Feel free to connect or contribute!  
🌐 [LinkedIn](https://www.linkedin.com/in/charliechen2698619/)


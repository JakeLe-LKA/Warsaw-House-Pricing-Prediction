# 🏘️ Warsaw House Price Prediction with Random Forest

## 📌 Project Overview
This project was developed as part of the premilinary task of ING Risk Modelling Challenge and focuses on predicting residential property prices in Warsaw, Poland. Accurate price estimation is critical for mortgage valuation, credit risk assessment, and real estate investment planning. 

**Technologies Used:**
- Python, pandas, numpy for data preprocessing
- scikit-learn (RandomForestRegressor)
- matplotlib, seaborn for visualization
- GenAI to support data construction and feature creation

---

## 🔍 Problem Statement
Poland's capital city, Warsaw, has a fast-developing real estate market influenced by urbanization, infrastructure investment, and sustainability policies. Our aim is to predict housing prices in Warsaw using interpretable and robust machine learning models, especially in the presence of limited or outdated data.

---

## 🧪 Data Pipeline & Feature Engineering

**Base Dataset:**
- 23.8k rows of apartment listings from Poland
- Filtered down to **8,926 listings in Warsaw**

**Key Preprocessing Steps:**
- Extract district from address
- Calculate:
  - `distance_to_nearest_metro`
  - `distance_to_pkin` (city center)
- Created synthetic indices:
  - `living_condition_index` – social/infrastructure score from 11 criteria
  - `es_index` – aggregated score of environmental & safety (air quality + crime rate)
- Converted `year` column into `age_of_house`
- Dropped irrelevant columns, ensured clean types, and added random noise to reduce district-level feature leakage

**Final Feature Set:**
- `sq`, `rooms`, `floor`, `age_of_house`
- `district`, `distance_to_pkin`, `distance_to_nearest_metro`
- `living_condition_index`, `es_index`

**All missing values handled**  
**Skewed distributions transformed** where needed

---

## 🏗️ Model Building

After comparing multiple models (Linear Regression, XGBoost), we selected **Random Forest Regressor** due to its:
- High performance on tabular data
- Robustness to outliers
- Interpretability via feature importance

**Target variable:** `price` (in PLN)

**Performance Metrics:**
| Metric | Value | Interpretation |
|--------|-------|----------------|
| R²     | 0.899 | ✅ Excellent |
| MAE    | 91,501 PLN (11.5%) | ⚠️ Moderate |
| RMSE   | 205,764 PLN (25.8%) | ❌ Poor (due to high-value outliers) |

**Key Insight:**  
The model performs well on **low-to-mid priced apartments**, but underestimates **high-end apartments** due to data imbalance.

---

## 📊 Feature Importance (Top Contributors)
1. `sq` (area of apartment)
2. `living_condition_index`
3. `distance_to_pkin`
4. `es_index` (environment + safety)
5. `district`

These factors align with real-world drivers of property valuation: space, accessibility, livability, and ESG trends.

---

## 📈 Model Sensitivity & Scalability

- **Increasing number of trees** improves MAE up to a certain point (diminishing return).
- **Training time and memory usage** rise linearly with data size.
- More data improves prediction quality—future work should focus on expanding dataset size.

---

## 🤖 Use of GenAI

GenAI supported the project by:
- Structuring the pipeline
- Helping define synthetic variables (`living_condition_index`, `es_index`)
- Accelerating feature enrichment with public data

However, the team **manually validated all outputs** to ensure quality and realism.

---

## 📌 Business Impact

This predictive model can support:
- Mortgage approval systems (Loan-to-Value)
- Dynamic property valuation tools
- ESG-conscious real estate investment
- Urban planning prioritization based on livability

---

## 🚧 Limitations & Future Work
- Dataset limited to 2021 → model may not generalize to newer trends
- ESG index lacks Governance component
- Price underestimation in high-end segment
- Room for model upgrades: SHAP explanations, Gradient Boosting, or Deep Learning

---

## 📂 Explore the Project
👉 Full notebook and source code available on this repository  

---

## Authors 
*Team: Flying Vietnamese – ING Risk Modelling Challenge 2024*

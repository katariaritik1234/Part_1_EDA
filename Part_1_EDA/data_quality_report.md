

# Data Quality Audit & Treatment Report

## Executive Summary
An exhaustive data quality audit was conducted across all provided datasets (`customers`, `orders`, `support_tickets`, `web_events_snapshot`, `churn_labels`, `intervention_history`, and `rfm_modeling_snapshot`). The audit evaluated missing values, duplicate records, join integrity, logical consistencies, and data leakage risks. 

Overall, relational integrity is structurally sound with zero orphaned records across tables. However, several critical data quality issues—specifically concerning data leakage, deliberate duplicates, and significant monetary outliers—must be resolved before proceeding with ML feature engineering or RFM segmentation.

---

## 1. Critical Issue: Target Leakage (Post-Snapshot Data)
**Observation:** The dataset contains a severe risk of target leakage. The defined snapshot date for feature engineering is `2025-09-30`. An audit of the `orders.csv` table revealed **1,872 orders** placed after this date. 
**Impact:** If these orders are included in RFM calculations, the predictive model will artificially "look into the future," violating strict no-leakage constraints and rendering the validation scores useless.
**Treatment Applied:** Strictly filtered the `orders` dataframe to drop any rows where `order_date > '2025-09-30'` prior to performing EDA and RFM feature generation.

---

## 2. Duplicate Records
**Observation:** A targeted ID check revealed **12 duplicate-like records** in the `orders.csv` table, specifically identified by the `_DUP` suffix in the `order_id` column.
**Impact:** Retaining these duplicate transactions artificially inflates the Frequency and Monetary (FM) scores for the affected customers.
**Treatment Applied:** Filtered out and dropped the 12 rows where `order_id` ends with `_DUP`.

---

## 3. Missing Values
**Observation:** Missing data was identified in three specific columns:
* **`customers` (loyalty_tier):** 1,386 missing values (57.8%).
* **`customers` (skin_type):** 401 missing values (16.7%).
* **`orders` (rating):** 80 missing values (0.8%).

**Impact:** Tree-based machine learning algorithms require explicit handling of `NaN` values to function correctly.
**Treatment Applied:** * `loyalty_tier`: Replaced `NaN` with the explicit string `"Not Enrolled"`.
* `skin_type`: Replaced `NaN` with `"Unknown"`.
* `rating`: Dropped from average rating calculations for those specific orders, to be imputed with the median in the ML pipeline.

---

## 4. Outliers & Extreme Values
**Observation:** An assessment of `gross_amount` revealed a significant right-skew. While the average order value is **₹744**, the maximum order value is **₹24,789.38**.
**Impact:** Extreme outliers heavily distort the "Monetary" axis of the RFM segmentation.
**Treatment Applied:** Identified for Winsorization (capping at the 99th percentile) during the formal preprocessing pipeline to stabilize model variance.

---

## 5. Logical Consistency & Join Integrity
**Observation:**
* **Join Integrity:** 100% of `customer_id` values in the `orders` and `support_tickets` tables successfully map back to the primary `customers` table (**0 orphaned records**).
* **Logical Boundaries:** The audit confirmed **0** negative web session counts, **0** negative ticket resolution hours, and **0** sentiment scores outside the valid `-1.0` to `1.0` range.

**Conclusion:** Aside from the isolated leakage and duplicate traps, the core relational logic is clean and reliable for advanced modeling.
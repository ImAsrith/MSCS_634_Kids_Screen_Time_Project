# MSCS 634 Kids Screen Time Project 
**Author:** Asrith Krishna Vejandla  
**Date:** 11th-13th July 2025  

## Dataset at a glance  
* **Source:** Kaggle – *Indian Kids ScreenTime 2025*  
* **Rows:** 9 668  *Columns:* 8 original + engineered  
* **Core fields** `Age · Gender · Urban_or_Rural · Avg_Daily_Screen_Time_hr · Primary_Device · Educational_to_Recreational_Ratio · Exceeded_Recommended_Limit · Health_Impacts`

---

## ▶ Deliverable 1 – Data Collection, Cleaning & Exploration  
*Notebook:* `Deliverable_1/Residency_Project.ipynb`  

| Stage | Summary | Insight |
|-------|---------|---------|
| **Loading & inspection** | Verified dtypes, ranges. | Screen-time hours highly right-skewed. |
| **Cleaning** | Filled missing `Health_Impacts` with “None”; median-imputed numeric gaps; removed three impossible ages; dropped duplicates. | Final tidy set: 9 668 rows × 8 cols. |
| **EDA visualisations** | Histograms · box-plots · correlation heat-map · Age vs Hours scatter. | Quantity (hours) and quality (edu-ratio) are largely independent, setting up orthogonal modelling axes. |

---

## ▶ Deliverable 2 – Regression Modelling  
*Notebook:* `Deliverable_2/Residency_Project.ipynb`

| Model | Features | Test R² | RMSE (hr) | Headline |
|-------|----------|---------|-----------|----------|
| Simple linear | Age | 0.018 | 1.66 | Age alone explains < 2 %. |
| Multiple linear | Age, gender, device, locale, ratio, interaction | 0.027 | 1.65 | Extra features add only marginal lift. |
| Ridge (α≈0.46) | same | 0.026 | **1.65** | Best error but still under-fits heavy users. |

*28 % of hold-out cases land within ±1 hour.*  
**Top drivers:** lower educational ratio ↑ hours; tablets add ≈0.6 hr; age adds ≈0.2 hr per year.

---

## ▶ Deliverable 3 – Classification · Clustering · Association Rules  
*Notebook:* `Deliverable_3/Residency_Project.ipynb`

### 3 · 1 Classification – Health-impact likelihood  
* Logistic Regression (OvR) and tuned Random-Forest (OvR, depth = 5).  
* Macro ROC-AUC ≈ 0.54–0.55; high recall but low precision → content mix and device matter, yet unseen lifestyle factors dominate.

### 3 · 2 Unsupervised Clustering – Usage archetypes  
* PCA (2D, 74 % variance) → K-Means (k = 3).  
* **Cluster 0 Light-Educational** (3 253) – low hours, high ratio, negligible complaints.  
* **Cluster 2 Balanced-Moderate** (3 306) – median hours, mixed content.  
* **Cluster 1 Heavy-Recreational** (3 109) – longest hours, lowest ratio, most eye-strain & sleep issues.  
* **Action:** prioritise targeted interventions for Cluster 1.

### 3 · 3 Association-Rule Mining – Behaviour → Health patterns  
* Apriori (support ≥ 5 %, conf ≥ 0.6, lift ≥ 1.2).  
* Rule example: *LowEduRatio & Device_Laptop ⇒ Poor Sleep* (conf 0.64 · lift 1.33).  
* Message: content quality in the 3–6 hr band is more predictive of complaints than extreme time alone.

---

## Ethical notes & limitations  
* **Missing context:** no bedtime stamps, distance-to-screen, or parental rules → models under-fit extremes.  
* **Class imbalance:** used `class_weight="balanced"` for rare labels.  
* **Privacy:** dataset is anonymised; no PII processed.  
* **Fairness:** recommendations target behaviours (device, ratio) rather than demographic identities.

---

## Reproducing the analysis  
1. Clone the repo and open any `Residency_Project.ipynb` in Colab or Jupyter.  
2. Run all cells; CSV is embedded in Deliverable 1 notebook.  
3. Plots and metrics regenerate automatically.




# MSCS 634 Kids Screen-Time Project  
**Author:** Asrith Krishna Vejandla  
**Updated:** 13 July 2025  

---

## Dataset at a glance  
* **Source:** Kaggle – *Indian Kids ScreenTime 2025*  
* **Rows:** 9668  *Columns:* 8 original + engineered  
* **Core fields** `Age · Gender · Urban_or_Rural · Avg_Daily_Screen_Time_hr · Primary_Device · Educational_to_Recreational_Ratio · Exceeded_Recommended_Limit · Health_Impacts`

---

## ▶ Deliverable 1 – Data Collection, Cleaning & Exploration  
*Notebook:* `Deliverable_1/Residency_Project.ipynb`  

| Stage | Summary | Insight |
|-------|---------|---------|
| Loading & inspection | Verified dtypes and ranges. | Screen-time hours are highly right-skewed. |
| Cleaning | Filled missing `Health_Impacts` with *None*, median-imputed numeric gaps, removed three impossible ages, dropped duplicates. | Final tidy set contains 9668 rows × 8 columns. |
| EDA visualisations | Histograms, box-plots, correlation heat-map, Age vs Hours scatter. | Quantity (hours) and quality (edu-ratio) behave independently, giving two modelling axes. |

---

## ▶ Deliverable 2 – Regression Modelling  
*Notebook:* `Deliverable_2/Residency_Project.ipynb`

| Model | Features | Test R² | RMSE (hr) | Headline |
|-------|----------|---------|-----------|----------|
| Simple linear | Age | 0.018 | 1.66 | Age alone explains < 2 %. |
| Multiple linear | Age, gender, device, locale, ratio, interaction | 0.027 | 1.65 | Extra features add little lift. |
| Ridge (α≈0.46) | Same set | 0.026 | **1.65** | Best error yet still under-fits heavy users. |

Twenty-eight percent of hold-out cases land within ±1 hour.  
Top drivers: lower educational ratio increases hours; tablets add about 0.6 hours; every additional year of age adds roughly 0.2 hours.

---

## ▶ Deliverable 3 – Classification, Clustering, Association Rules  
*Notebook:* `Deliverable_3/Residency_Project.ipynb`

### 3.1 Classification – Health-impact likelihood  
Logistic Regression and tuned Random-Forest (OvR) give macro ROC–AUC ≈ 0.55.  
Risk rises with tablet use and low educational ratio, confirming that content quality outweighs raw hours.

### 3.2 Unsupervised Clustering – Usage archetypes  
PCA (2 D, 74 % variance) followed by K-Means (k = 3) yields  
Light-educational, Balanced-moderate, and Heavy-recreational tribes.  
Heavy-recreational users log the longest hours, lowest quality, and most complaints.

### 3.3 Association-Rule Mining – Behaviour ↔ Health  
Apriori rules with lift > 1.2 show that *LowEduRatio* combined with laptops or smartphones predicts poor sleep and eye strain even at moderate three-to-six-hour exposure.

---

## ▶ Deliverable 4 – Final Report & Presentation  
*Files:*  

* `Deliverable_4/ScreenTime_Final_Report.pdf` – Full APA-7 report: introduction, cleaned-data rationale, modelling results, ethical considerations, and recommendations.  
* `Deliverable_4/Residency_Project.ipynb` – Consolidated notebook that re-runs every step from raw import to final visuals.  


**Key take-aways**  
* Quality buffers risk: children whose screen time is at least sixty percent educational report markedly fewer complaints, even at longer durations.  
* Three usage tribes allow tiered interventions: maintain habits for light learners, nudge balanced users, target heavy recreational users with stricter controls.  
* Recommendations focus on shifting content mix and adding device-level prompts rather than blanket time bans.  

---

## Ethical notes & limitations  
* Missing context (bedtime use, brightness, parental rules) limits predictive power.  
* Class imbalance handled with `class_weight="balanced"`; no demographic feature alone drives negative outcomes.  
* Dataset is anonymised; the project targets modifiable behaviours, not identities.

---

## Reproducing the analysis  
1. Clone or download the repository.  
2. Open the consolidated notebook in `Deliverable_4` and run all cells; the data file is included.  
3. Review the final PDF report and play the presentation video for a narrated summary.



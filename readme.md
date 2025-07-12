# MSCS_634_ProjectDeliverable_1

## Dataset  
**Indian Kids ScreenTime 2025**  
- **Records:** 9,712  
- **Features (8):**  
  - `Age` (8–18 years)  
  - `Gender`  
  - `Avg_Daily_Screen_Time_hr`  
  - `Primary_Device`  
  - `Exceeded_Recommended_Limit` (Yes/No)  
  - `Educational_to_Recreational_Ratio` (0–1)  
  - `Health_Impacts` (e.g. Anxiety, Poor sleep, Eye Strain, and “None”)  
  - `Urban_or_Rural`

## Cleaning Steps  
1. **Missing values**  
   - Filled `Health_Impacts` NaNs with `"None"`.  
   - Imputed numeric gaps (e.g. screen time) with column medians.  
   - Filled categorical gaps (e.g. `Primary_Device`) with mode.  
2. **Duplicates**  
   - Removed exact duplicate rows.  
3. **Inconsistent data**  
   - Dropped rows where `Age` was outside 8–18 years (n = 3).

## Exploratory Data Analysis  
- **Distribution**  
  - Avg daily screen time is right-skewed (median ≈ 4 hr, IQR ≈ 3–6 hr) with a long tail to 14 hr.  
- **Outliers**  
  - Genuine heavy-use cases (> 8 hr) retained for later modelling.  
- **Correlations**  
  - `Age` vs. screen time: weak positive (ρ≈0.11).  
  - `Age` vs. educational ratio: moderate negative (ρ≈–0.49).  
  - `Ratio` vs. screen time: near zero (ρ≈–0.08), indicating independent dimensions.  
- **Age vs. Screen Time Scatter**  
  - Youngest children (8–10) show the widest variation, including extreme high values.

## Key Insights  
1. **Quantity vs. Quality**  
   - “How long” (hrs/day) and “how educational” (ratio) behave independently—both merit separate modelling.  
2. **Age patterns**  
   - Older teens tend toward consistent mid-range use; younger kids vary more.  
3. **Model prep**  
   - Skewed `Avg_Daily_Screen_Time_hr` may benefit from a log transform.  
   - Binning `Age` into stages (8–10, 11–13, 14–18) could capture non-linear effects.

## Challenges  
- Configuring Colab file upload vs. Kaggle API—opted for manual CSV upload for speed.  
- A few out-of-range ages required domain-based exclusion.

## Next Steps  
- **Deliverable 2:** Build regression models to predict screen time.  
- **Deliverable 3:** Classify “heavy users” and cluster usage archetypes.  
- **Deliverable 4:** Derive actionable recommendations and discuss ethical implications.

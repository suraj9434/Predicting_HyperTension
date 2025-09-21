# Predicting Hypertension (Framingham Study)

**Author:** Suraj Shrestha

---

## Project Overview

Hypertension is a leading risk factor for cardiovascular disease.  
Using data from the **Framingham Heart Study (n = 11,627)**, this project develops predictive models to identify individuals at risk of prevalent hypertension (**PREVHYP**).

This project highlights:

- Detecting and correcting **data leakage**  
- Application of **Logistic Regression** and **Random Forests**  
- Alignment of predictive insights with **clinical knowledge**  

📄 **Full Report (PDF):** [Predicting_HyperTension.pdf](./Predicting_HyperTension.pdf)

---

## Data & Approach

- **Data Source:** Framingham Heart Study, a longitudinal cardiovascular cohort.  
- **Target Variable:** `PREVHYP` (binary: 0 = no, 1 = yes).  
- **Predictors:** Demographics, cholesterol, BMI, blood pressure, smoking, diabetes, and other cardiovascular risk factors.  

**Challenge:**  
Several variables (e.g., `TIMEHYP`, `HYPERTEN`) directly encoded the outcome, leading to artificially perfect models.  

**Solution:**  
These leakage variables were removed, and models were re-trained using **5-fold cross-validation**.

---

## Key Results

### Model 1 — Before Fixing Leakage
- Logistic Regression & Random Forest appeared to achieve **100% accuracy and AUC = 1.0**.  
- This was unrealistic and confirmed reliance on outcome-related leakage variables.

### Model 2 — After Fixing Leakage
- **Logistic Regression:** Accuracy ≈ **87%**, AUC = **0.939**  
- **Random Forest:** Accuracy ≈ **88%**, AUC = **0.943**  
- Sensitivity and specificity both ≥84–88%.  
- Random Forest slightly outperformed Logistic Regression, but both were strong and clinically meaningful.

### Variable Importance
- Top predictors: **Systolic BP (SYSBP)**, **Diastolic BP (DIABP)**, **Age**, **BMI**, and **Blood Pressure Medication Use**.  
- These align with established medical knowledge, supporting clinical validity.

---

## Repository Contents

- `Predicting_Hypertension.Rmd` — R Markdown code for data cleaning, modeling, and evaluation.  
- `Predicting_HyperTension.pdf` — Final report with methods, results, and visualizations.  
- `frmgham.csv` — Dataset (subset of the Framingham Heart Study).  

---

## Tools & Libraries

This analysis was conducted in **R** using RStudio. Key packages include:

- `tidyverse` — data manipulation  
- `tidymodels` — recipes, workflows, cross-validation, tuning  
- `glmnet` — logistic regression with regularization  
- `ranger` — random forest modeling  
- `pROC` — ROC curves and AUC evaluation  
- `vip` — variable importance plots  

---

## How to Run This Project

```bash
1. Clone the repository:
   git clone <repository-url>
   cd Predicting-Hypertension

2. Install required packages in R:
   install.packages(c("tidyverse", "tidymodels", "glmnet", "ranger", "pROC", "vip", "knitr"))

3. Download and place dataset:
   Ensure frmgham.csv is in the project root folder.

4. Run analysis:
   Open Predicting_Hypertension.Rmd in RStudio and click Knit to generate the full PDF report.
```

## Limitations

- The dataset is observational and limited to the Framingham cohort.  
- Results may not generalize to broader populations.  
- Additional clinical variables (e.g., diet, exercise, genetics) could improve predictive power.  

---

## Conclusion

After correcting for data leakage, both Logistic Regression and Random Forest achieved high accuracy and AUC values (≈0.94).  
The models identified well-established clinical predictors of hypertension, confirming that the approach is **both statistically robust and medically meaningful**.

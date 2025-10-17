# Understanding Depression Risk Through Demographics, Clinical Factors & Mindfulness Interventions

This repository contains the complete analysis for the IEEE BHI 2025 Data Challenge submission by Team Blackout. The project focuses on developing interpretable machine learning models to predict depression severity (measured by BDI-II scores) at 12 and 24 weeks. Our analysis identifies key influential factors, explores their temporal shifts, and provides a granular, disease-specific comparison of risk profiles.

The final report can be found here: [**Final_Report.pdf**](IEEE_BHI_2025_Data_Challenge_Team_Blackout_Final_Report.pdf) 📄

---

##  Methodological Approach

The core of our analysis was to build robust predictive models while handling a significant amount of missing data in the target variables. Our final approach involved a multi-stage process:

1.  **Data Preprocessing:** Cleaning data, one-hot encoding categorical variables, and engineering a `session_completion_rate` feature.
2.  **Stochastic Imputation:** Using a Random Forest "helper" model to impute missing BDI-II scores, preserving sample size and data variance. This was a critical step that dramatically improved model performance over simpler methods.
3.  **Comprehensive Modeling:** Evaluating a suite of models, including Ridge Regression, LightGBM, XGBoost, Random Forest, and CatBoost.
4.  **In-depth Interpretation:** Performing three key analyses to uncover nuanced insights:
    * **Temporal Impact Analysis:** Comparing 12-week vs. 24-week predictors.
    * **Disease-Specific Comparison:** Training dedicated models for distinct clinical subgroups.
    * **Hierarchical Analysis:** Investigating predictor differences within subtypes of a single disease (e.g., Breast vs. Prostate cancer).

---

## 📂 Repository Structure

This repository is organized into three main Jupyter Notebooks, each representing a different stage or approach in our analysis.

### 1. `main.ipynb`
* **Purpose:** Initial baseline modeling.
* **Methodology:** This notebook takes the most direct approach by simply dropping all patient rows with missing target values (listwise deletion).
* **Outcome:** The models trained on this severely reduced dataset performed poorly, yielding negative R² scores. This notebook serves as a crucial baseline that demonstrates why more sophisticated data handling was necessary.

### 2. `main_with_imputation.ipynb`
* **Purpose:** **This is the primary notebook for the final analysis and contains all the results presented in our report.** 🏆
* **Methodology:** Implements our robust stochastic imputation strategy to preserve the full dataset. It then proceeds with all subsequent analyses:
    * Global model training and evaluation.
    * Temporal impact analysis (12w vs. 24w).
    * Disease-specific comparisons across all subgroups.
    * Hierarchical analysis of cancer and renal subtypes.
    * Generation of all final plots for the report.

### 3. `main_ridge_no_Imputation_Hyperparameter_tuning.ipynb`
* **Purpose:** An alternative modeling approach used for methodological justification.
* **Methodology:** This notebook explores a different strategy: using Ridge Regression for feature selection, followed by listwise deletion and hyperparameter tuning.
* **Outcome:** While performance was better than the simple baseline, it was still significantly inferior to the imputation approach. The results from this notebook are referenced in the "Methodology" section of our report to justify our final choice of using imputation.

---

## 🚀 How to Run

To replicate the analysis, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repository-name.git](https://github.com/your-username/your-repository-name.git)
    cd your-repository-name
    ```
2.  **Set up a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Run the notebooks:**
    * For the main results, run the cells in **`main_with_imputation.ipynb`**.
    * To see the baseline and alternative approaches, explore `main.ipynb` and `main_ridge_no_Imputation_Hyperparameter_tuning.ipynb`.

---

## ✨ Key Findings

Our analysis uncovered several actionable insights:
* **Temporal Shift:** Clinical context is paramount for short-term outcomes, but long-term success is more closely tied to **behavioral adherence** and demographic factors like **age**.
* **Disease Heterogeneity:** A "one-size-fits-all" model is insufficient. Different clinical conditions (e.g., Acute Coronary Syndrome vs. Breast Cancer) are driven by entirely different risk factors.
* **Hierarchical Nuance:** Even within a single disease like cancer, the predictors for subtypes (Breast vs. Prostate) vary significantly, strengthening the case for personalized interventions.

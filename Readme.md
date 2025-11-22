### Nanoparticle Toxicity Modeling and Interpretability Analysis

This repository contains a complete data analysis pipeline for modeling and interpreting silver nanoparticle (AgNP) toxicity. The goal is to predict the **Minimum Inhibitory Concentration (MIC)** based on AgNP physicochemical properties (size, shape, synthesis method) and the target bacterium's Gram stain.

The core of this project uses the **XGBoost (eXtreme Gradient Boosting)** model, selected for its high accuracy on complex and non-linear data. Model interpretability is achieved using **SHAP (SHapley Additive exPlanations)** to understand the model's predictions.

### Key Project Components

1.  **Data Cleaning and Transformation:** Loading and cleaning the `Ag_MIC_Database.csv` file, including helper functions to standardize the `Size (nm)` and `MIC (µg/mL)` columns, and categorizing the `Synthesis Method`. A log10 transformation is applied to the target variable (MIC) due to its highly skewed distribution.
2.  **XGBoost Modeling:** Training and tuning an XGBoost Regressor using `RandomizedSearchCV` to predict the log-transformed MIC.
3.  **Model Performance:** The final main model achieved a performance of **$R^{2} \approx 0.70$** in the log-transformed space, indicating it explains nearly 70% of the variance.
4.  **Interpretability Analysis (SHAP):** Using SHAP to move beyond simple feature importance and explore:
      * Deep Non-Linear Effects
      * Feature Interactions 
      * Conditional Toxicity (Gram-Positive vs. Gram-Negative) 
5.  **Validation of Non-Linearity:** Testing alternative models (Lasso, Ridge, SVR) which completely failed (R^2 = 0.0 or negative), strongly confirming the relationship is highly non-linear, justifying the choice of XGBoost.
6.  **Sub-Population Analysis:** Training independent models for Gram-Negative and Gram-Positive bacteria to check if the rules for toxicity change between populations.

### Setup and Usage

The analysis pipeline is contained within a Jupyter Notebook.

**Prerequisites:**

You will need the following libraries, which can typically be installed via pip:

```bash
pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn
```

**Files:**

  * `final_MIC_AgNP.ipynb`: The main Jupyter Notebook containing the entire analysis pipeline.
  * `Ag_MIC_Database.csv`: The dataset containing AgNP toxicity data (not included, assumed to be available locally).

### Key Scientific Findings

Based on the SHAP analysis:

| Feature | Trend in SHAP Analysis | Impact on MIC (Toxicity) |
| :--- | :--- | :--- |
| **Size (nm)** | High feature values (large size, red dots) produce positive SHAP values. | **Primary driver of high MIC (low toxicity)**. |
| **Synthesis Method\_chemical** | Highly associated with positive SHAP values. | **Strongly drives high MIC (low toxicity)**. |
| **Shape\_Cubic** | Associated with positive SHAP values. | **Contributes to high MIC (low toxicity)**. |

**Sub-Population Insight:**
The separate XGBoost models trained on Gram-Negative and Gram-Positive bacteria showed similar trends, indicating that the physicochemical properties of the silver nanoparticles do not significantly change their mechanism of action between the two bacterial populations.

### Data Source & Citation

This analysis utilizes a publicly available dataset on AgNP toxicity.


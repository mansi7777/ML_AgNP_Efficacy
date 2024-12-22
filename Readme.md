
### Nanoparticle Toxicity Modeling and Interpretability Analysis

[cite\_start]This repository contains a complete data analysis pipeline for modeling and interpreting silver nanoparticle (AgNP) toxicity[cite: 5]. [cite\_start]The goal is to predict the **Minimum Inhibitory Concentration (MIC)** based on AgNP physicochemical properties (size, shape, synthesis method) and the target bacterium's Gram stain[cite: 6].

[cite\_start]The core of this project uses the **XGBoost (eXtreme Gradient Boosting)** model, selected for its high accuracy on complex and non-linear data[cite: 7]. [cite\_start]Model interpretability is achieved using **SHAP (SHapley Additive exPlanations)** to understand the model's predictions[cite: 8].

### Key Project Components

1.  [cite\_start]**Data Cleaning and Transformation:** Loading and cleaning the `Ag_MIC_Database.csv` file, including helper functions to standardize the `Size (nm)` and `MIC ($\mu g/mL$)` columns, and categorizing the `Synthesis Method`[cite: 41]. [cite\_start]A $log_{10}$ transformation is applied to the target variable (MIC) due to its highly skewed distribution[cite: 102].
2.  [cite\_start]**XGBoost Modeling:** Training and tuning an XGBoost Regressor using `RandomizedSearchCV` to predict the log-transformed MIC[cite: 126, 127].
3.  [cite\_start]**Model Performance:** The final main model achieved a performance of **$R^{2} \approx 0.70$** in the log-transformed space, indicating it explains nearly 70% of the variance[cite: 131, 172].
4.  **Interpretability Analysis (SHAP):** Using SHAP to move beyond simple feature importance and explore:
      * [cite\_start]Deep Non-Linear Effects [cite: 10]
      * [cite\_start]Feature Interactions [cite: 11]
      * [cite\_start]Conditional Toxicity (Gram-Positive vs. Gram-Negative) [cite: 12]
5.  [cite\_start]**Validation of Non-Linearity:** Testing alternative models (Lasso, Ridge, SVR) which completely failed ($R^{2} \approx 0.0$ or negative), strongly confirming the relationship is highly non-linear, justifying the choice of XGBoost[cite: 237, 238].
6.  [cite\_start]**Sub-Population Analysis:** Training independent models for Gram-Negative and Gram-Positive bacteria to check if the rules for toxicity change between populations[cite: 12, 268].

### 💻 Setup and Usage

The analysis pipeline is contained within a Jupyter Notebook.

**Prerequisites:**

You will need the following libraries, which can typically be installed via pip:

```bash
pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn
```

**Files:**

  * `final_MIC_AgNP.ipynb`: The main Jupyter Notebook containing the entire analysis pipeline.
  * `Ag_MIC_Database.csv`: The dataset containing AgNP toxicity data (not included, assumed to be available locally).

### 🔍 Key Scientific Findings

Based on the SHAP analysis:

| Feature | Trend in SHAP Analysis | Impact on MIC (Toxicity) |
| :--- | :--- | :--- |
| **Size (nm)** | [cite\_start]High feature values (large size, red dots) produce positive SHAP values[cite: 200]. | [cite\_start]**Primary driver of high MIC (low toxicity)**[cite: 200, 192]. |
| **Synthesis Method\_chemical** | [cite\_start]Highly associated with positive SHAP values[cite: 201]. | [cite\_start]**Strongly drives high MIC (low toxicity)**[cite: 201, 192]. |
| **Shape\_Cubic** | [cite\_start]Associated with positive SHAP values[cite: 202]. | [cite\_start]**Contributes to high MIC (low toxicity)**[cite: 202, 192]. |

**Sub-Population Insight:**
[cite\_start]The separate XGBoost models trained on Gram-Negative and Gram-Positive bacteria showed similar trends, indicating that the physicochemical properties of the silver nanoparticles do not significantly change their mechanism of action between the two bacterial populations[cite: 271].

### 📜 Data Source & Citation

[cite\_start]This analysis utilizes a publicly available dataset on AgNP toxicity[cite: 14].


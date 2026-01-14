# US Healthcare Premium Analysis (Survey-Weighted GLM)
This project analyzes data from the 2024 National Health Interview Survey (NHIS) to identify the demographic, socioeconomic, and health-related factors that drive private health insurance premium costs in the United States.

Using R, we performed a complete statistical analysis pipeline—from data cleaning and complex survey design implementation to generalized linear modeling (GLM) and variable selection. The final model quantifies how factors like anxiety, sexual orientation, and lifestyle choices impact insurance costs.
Based on the comprehensive report and R code you provided, here is a structured draft for your GitHub README. This is designed to highlight the technical rigor of the project (specifically the survey-weighted analysis and custom feature selection) to appeal to data science recruiters.

* **Sexual Orientation:** Surprisingly, gay/lesbian individuals face significantly higher premiums compared to straight individuals.


* **Mental Health:** Daily anxiety was found to be a statistically significant driver of higher costs.


*  **Lifestyle:** Healthy behaviors (exercise, quitting drinking/smoking) correlate with lower premiums.


*  **Socioeconomics:** Higher education levels were associated with higher premiums, likely due to the correlation with better/more comprehensive insurance plans.


<img width="883" height="546" alt="image" src="https://github.com/user-attachments/assets/4a3b5529-e16f-46b4-b94c-8ff829482a4e" />

*Figure: Estimated % Impact on Premium Costs (Gamma GLM)*

### **Methodology**

#### **1. Data Cleaning & Preprocessing**

* Filtered a dataset of 30,000+ respondents down to ~6,421 sample adults with private insurance and no dependents to isolate individual premium costs.


* Handled 600+ covariates, filtering for non-response (NA/Refused) and converting categorical variables to factors.



#### **2. Model Selection & Diagnostics**

* **Initial Approach:** Attempted OLS Linear Regression. Diagnostics (Residuals vs. Fitted, Q-Q Plot) revealed strong heteroscedasticity and right-skewed residuals.


* 
**Solution:** Implemented a **Gamma GLM with a Log Link function**, which appropriately handles skewed, positive-only cost data.


* 
**Survey Design:** Utilized the `survey` package in R to incorporate stratification (`PSTRAT`), clustering (`PPSU`), and sampling weights (`WTFA_A`) to ensure population-level unbiased estimates.


#### **3. Refinement**

*  **Multicollinearity:** Checked Cramer’s V to remove highly correlated categorical predictors (e.g., removing `RACEALLP` in favor of `HISPALLP`).


*  **Outlier Removal:** Used Cook’s Distance to identify and remove influential observations, reducing the dispersion parameter from 13.92 to 1.19.
  

#### **4. Advanced Feature Selection (Custom Implementation)**

Standard AIC/BIC selection methods (like `stepAIC`) are not valid for survey-weighted designs because they lack a standard likelihood estimator.

* **Solution:** We wrote custom R functions to perform **Forward, Backward, and Hybrid stepwise selection** using **Wald's Test** to evaluate variable significance.


* **Result:** The backward selection method yielded the optimal model with 13 significant predictors.

  

### **Technologies Used**

* **R** (Primary analysis)
* **Libraries:** `survey` (complex survey design), `tidyverse` (data manipulation), `ggplot2` (visualization), `lawstat`, `car`, `broom`.
* **Statistical Concepts:** Generalized Linear Models (GLM), Survey Weighting, Wald Tests, Multicollinearity (Cramer's V), Homoscedasticity.

### **Credits**

Project completed by Thomas Stranick, Mohan Askani, and Avi Kodali.

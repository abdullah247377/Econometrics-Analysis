# Econometrics-Analysis
Fixed Effects Regression Model with Clustered Standard Errors to control for unobserved country-specific heterogeneity.

## Impact of Digital Trade Openness on Foreign Direct Investment (FDI)
<img width="780" height="317" alt="Screen Shot 2026-08-16 at 9 27 21 PM" src="https://github.com/user-attachments/assets/d5406fca-5c62-4199-9e90-0587e51b9d35" />

**Author:** Abdullah Anayat  

## 📌 Project Overview
This project investigates the impact of digital trade openness on Foreign Direct Investment (FDI) inflows across 15 countries from 2015 to 2024. As the global economy undergoes rapid digital transformation, understanding how digital regulatory environments—specifically restrictions on digital trade—affect multinational investment decisions is critical. 

This repository demonstrates an end-to-end econometric workflow, from data imputation and exploratory data analysis (EDA) to advanced panel data modeling using Fixed Effects with Clustered Standard Errors.

## 🛠️ Statistical & Econometric approaches used:
*   **Data Imputation:** Handled missing time-series data using linear interpolation (`pandas.DataFrame.interpolate`).
*   **Diagnostic Testing:** 
    *   **Multicollinearity:** Variance Inflation Factor (VIF).
    *   **Heteroskedasticity:** Breusch-Pagan Test.
    *   **Autocorrelation:** Durbin-Watson Test.
*   **Model Selection:** Hausman Specification Test to decide between Fixed Effects (FE) and Random Effects (RE).
*   **Robust Estimation:** Applied Country Clustered Standard Errors to correct for both heteroskedasticity and positive serial correlation.
*   **Tools Used:** Python (`pandas`, `seaborn`, `statsmodels`, `linearmodels`, `scipy`).

## 📊 Data Description
The analysis utilizes panel data merging macroeconomic indicators with digital trade restrictiveness. The raw dataset is available in the repository as `econ pdata.xlsx`.

| Variable | Description | Source |
| :--- | :--- | :--- |
| **FDI (Dependent)** | Net Inflows as % of GDP | World Bank (WDI) |
| **DSTRI (Independent)** | Digital Services Trade Restrictiveness Index (0 = Open, 1 = Closed) | OECD (2024) |
| **GDP Per Capita** | Current US$ (Proxy for Market Size) | World Bank (WDI) |
| **Trade Openness** | Sum of Exports & Imports as % of GDP | World Bank (WDI) |
| **Inflation** | Annual Consumer Prices (%) | World Bank (WDI) |
| **Internet Penetration** | Individuals using the Internet (% of population) | World Bank (WDI) |

## 🔬 Econometric Model
Grounded in Dunning’s Eclectic Paradigm (OLI Framework) and Transaction Cost Theory, the baseline panel regression model is specified as:

$$FDI_{it} = \beta_0 + \beta_1 DSTRI_{it} + \beta_2 GDPC_{it} + \beta_3 TRO_{it} + \beta_4 INF_{it} + \beta_5 IP_{it} + \alpha_i + \epsilon_{it}$$

Where $\alpha_i$ represents unobserved country-specific fixed effects and $\epsilon_{it}$ is the error term.

## 📈 Exploratory Data Analysis
Prior to modeling, data distributions and bivariate relationships were analyzed to check for outliers and linear dependencies. 


### Correlation Matrix
<img width="431" height="309" alt="Picture 1" src="https://github.com/user-attachments/assets/d2799e65-78dd-42bd-95c4-a674dd17700e" />
*Initial observations show a weak negative correlation (-0.10) between DSTRI and FDI, providing preliminary support for the hypothesis that higher restrictions associate with lower FDI.*

### Outlier Detection (Standardized)
<img width="1180" height="609" alt="Screen Shot 2026-08-16 at 9 21 14 PM" src="https://github.com/user-attachments/assets/a7a91aac-14c0-4700-b262-29ba385e19d0" />

## 🧪 Diagnostics & Model Selection
<img width="776" height="210" alt="Screen Shot 2026-08-16 at 9 21 30 PM" src="https://github.com/user-attachments/assets/d97c84f7-7d4e-4a3d-b7bc-2ad6fa22122d" />


A rigorous diagnostic pipeline was executed to ensure the validity of the OLS assumptions:
1.  **VIF Test:** All variables yielded a VIF < 5 (Max: GDP per Capita at 3.81), confirming no severe multicollinearity.
2.  **Breusch-Pagan Test:** ($p = 0.00032$) Rejected the null hypothesis of homoskedasticity.
3.  **Durbin-Watson Test:** Statistic of 1.3598 indicated the presence of positive autocorrelation.
4.  **Hausman Test:** ($p = 0.0000$) Strongly rejected the Random Effects assumption, dictating the use of a **Fixed Effects (FE) model**.

Because both heteroskedasticity and autocorrelation were detected, standard OLS errors would be biased. Therefore, the final FE model was estimated using **Clustered Standard Errors** at the country level to ensure robust statistical inference.

## 💡 Findings
*   **Primary Finding:** The coefficient for DSTRI was negative (-1.3509), suggesting that increased digital trade restrictions theoretically discourage FDI. However, this effect was **not statistically significant** ($p = 0.8703$) in this sample.
*   **Macroeconomic Drivers:** Traditional economic drivers, specifically GDP per capita ($p = 0.0641$) and Trade Openness ($p = 0.0665$), showed marginal statistical significance, indicating they remain the overriding influencers of FDI.
*   **Policy Implication:** Digital trade openness currently acts as a complementary factor rather than a standalone magnet for FDI. Policymakers must pursue a balanced approach, pairing digital liberalization with strong macroeconomic stability.

### Limitations & Assumptions
*   **Cluster Count:** The sample size is limited to 15 countries due to DSTRI data availability. Utilizing clustered standard errors on a small number of clusters ($N < 30$) can artificially inflate standard errors, making statistical significance harder to detect.
*   **Endogeneity/Reverse Causality:** The model assumes DSTRI impacts FDI, but there is a potential "chicken and egg" dynamic where high FDI inflows might drive a country to adopt more open digital policies.
*   **Imputation Smoothing:** Linear interpolation was used to fill gaps in the dataset. This assumes a constant rate of change between known points, which may smooth out the impact of volatile, real-world macroeconomic shocks.

### Repo Guide
**Folder Structure:**
*   `📁 data/`: Contains the final raw dataset (`econ pdata.xlsx`) used for the analysis (before processing).
*    The Jupyter notebook (`econ project analysis final.ipynb`) with the full data cleaning, EDA, and econometric modeling workflow.
*   `📁 docs/`: Contains the final analytical report and presentation slide deck.

## 🚀 How to Run the Code
1. Clone the repository: `git clone https://github.com/yourusername/digital-trade-fdi.git`
2. Install the required dependencies: `pip install pandas numpy seaborn matplotlib statsmodels linearmodels scipy`
3. Open `notebooks/econometrics_analysis.ipynb` in Jupyter and execute the cells sequentially.

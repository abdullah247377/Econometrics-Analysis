# Econometrics-Analysis
Fixed Effects Regression Model with Clustered Standard Errors to control for unobserved country-specific heterogeneity.

## Impact of Digital Trade Openness on Foreign Direct Investment (FDI)
<img width="780" height="317" alt="Screen Shot 2026-08-16 at 9 27 21 PM" src="https://github.com/user-attachments/assets/d5406fca-5c62-4199-9e90-0587e51b9d35" />

**Author:** Abdullah Anayat  

## 📌 Project Overview
This project investigates the impact of digital trade openness on Foreign Direct Investment (FDI) inflows across 15 countries from 2015 to 2024[cite: 1]. As the global economy undergoes rapid digital transformation, understanding how digital regulatory environments—specifically restrictions on digital trade—affect multinational investment decisions is critical[cite: 4]. 

This repository demonstrates an end-to-end econometric workflow, from data imputation and exploratory data analysis (EDA) to advanced panel data modeling using Fixed Effects with Clustered Standard Errors[cite: 1, 2].

## 🛠️ Statistical & Econometric approaches used:
*   **Data Imputation:** Handled missing time-series data using linear interpolation (`pandas.DataFrame.interpolate`)[cite: 2].
*   **Diagnostic Testing:** 
    *   **Multicollinearity:** Variance Inflation Factor (VIF)[cite: 1].
    *   **Heteroskedasticity:** Breusch-Pagan Test[cite: 1].
    *   **Autocorrelation:** Durbin-Watson Test[cite: 1].
*   **Model Selection:** Hausman Specification Test to decide between Fixed Effects (FE) and Random Effects (RE)[cite: 1].
*   **Robust Estimation:** Applied Country Clustered Standard Errors to correct for both heteroskedasticity and positive serial correlation[cite: 1, 2].
*   **Tools Used:** Python (`pandas`, `seaborn`, `statsmodels`, `linearmodels`, `scipy`)[cite: 2].

## 📊 Data Description
The analysis utilizes panel data merging macroeconomic indicators with digital trade restrictiveness[cite: 1]. The raw dataset is available in the repository as `econ pdata.xlsx`[cite: 1].

| Variable | Description | Source |
| :--- | :--- | :--- |
| **FDI (Dependent)** | Net Inflows as % of GDP | World Bank (WDI)[cite: 4] |
| **DSTRI (Independent)** | Digital Services Trade Restrictiveness Index (0 = Open, 1 = Closed) | OECD (2024)[cite: 4] |
| **GDP Per Capita** | Current US$ (Proxy for Market Size) | World Bank (WDI)[cite: 4] |
| **Trade Openness** | Sum of Exports & Imports as % of GDP | World Bank (WDI)[cite: 4] |
| **Inflation** | Annual Consumer Prices (%) | World Bank (WDI)[cite: 4] |
| **Internet Penetration** | Individuals using the Internet (% of population) | World Bank (WDI)[cite: 4] |

## 🔬 Econometric Model
Grounded in Dunning’s Eclectic Paradigm (OLI Framework) and Transaction Cost Theory, the baseline panel regression model is specified as[cite: 1, 4]:

$$FDI_{it} = \beta_0 + \beta_1 DSTRI_{it} + \beta_2 GDPC_{it} + \beta_3 TRO_{it} + \beta_4 INF_{it} + \beta_5 IP_{it} + \alpha_i + \epsilon_{it}$$

Where $\alpha_i$ represents unobserved country-specific fixed effects and $\epsilon_{it}$ is the error term[cite: 1].

## 📈 Exploratory Data Analysis
Prior to modeling, data distributions and bivariate relationships were analyzed to check for outliers and linear dependencies[cite: 2]. 


### Correlation Matrix
<img width="431" height="309" alt="Picture 1" src="https://github.com/user-attachments/assets/d2799e65-78dd-42bd-95c4-a674dd17700e" />
*Initial observations show a weak negative correlation (-0.10) between DSTRI and FDI, providing preliminary support for the hypothesis that higher restrictions associate with lower FDI.*[cite: 1]

### Outlier Detection (Standardized)
<img width="1180" height="609" alt="Screen Shot 2026-08-16 at 9 21 14 PM" src="https://github.com/user-attachments/assets/a7a91aac-14c0-4700-b262-29ba385e19d0" />

## 🧪 Diagnostics & Model Selection
<img width="776" height="210" alt="Screen Shot 2026-08-16 at 9 21 30 PM" src="https://github.com/user-attachments/assets/d97c84f7-7d4e-4a3d-b7bc-2ad6fa22122d" />

A rigorous diagnostic pipeline was executed to ensure the validity of the OLS assumptions[cite: 1]:
1.  **VIF Test:** All variables yielded a VIF < 5 (Max: GDP per Capita at 3.81), confirming no severe multicollinearity[cite: 1].
2.  **Breusch-Pagan Test:** ($p = 0.00032$) Rejected the null hypothesis of homoskedasticity[cite: 1, 2].
3.  **Durbin-Watson Test:** Statistic of 1.3598 indicated the presence of positive autocorrelation[cite: 1, 2].
4.  **Hausman Test:** ($p = 0.0000$) Strongly rejected the Random Effects assumption, dictating the use of a **Fixed Effects (FE) model**[cite: 1, 2].

Because both heteroskedasticity and autocorrelation were detected, standard OLS errors would be biased. Therefore, the final FE model was estimated using **Clustered Standard Errors** at the country level to ensure robust statistical inference[cite: 1].

## 💡 Findings
*   **Primary Finding:** The coefficient for DSTRI was negative (-1.3509), suggesting that increased digital trade restrictions theoretically discourage FDI. However, this effect was **not statistically significant** ($p = 0.8703$) in this sample[cite: 1, 4].
*   **Macroeconomic Drivers:** Traditional economic drivers, specifically GDP per capita ($p = 0.0641$) and Trade Openness ($p = 0.0665$), showed marginal statistical significance, indicating they remain the overriding influencers of FDI[cite: 1, 4].
*   **Policy Implication:** Digital trade openness currently acts as a complementary factor rather than a standalone magnet for FDI. Policymakers must pursue a balanced approach, pairing digital liberalization with strong macroeconomic stability[cite: 1, 4].

## 🚀 How to Run the Code
1. Clone the repository: `git clone https://github.com/yourusername/digital-trade-fdi.git`
2. Install the required dependencies: `pip install pandas numpy seaborn matplotlib statsmodels linearmodels scipy`
3. Open `notebooks/econometrics_analysis.ipynb` in Jupyter and execute the cells sequentially.

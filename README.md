# Time-Varying Correlation Between Commodity Prices: A DCC-GARCH Model Analysis

## Project Overview
This project investigates the dynamic correlations between key commodity futures (gold, crude oil, and corn) before and after the onset of the Russian-Ukrainian war. Using the Dynamic Conditional Correlation Generalized Autoregressive Conditional Heteroskedasticity (DCC-GARCH) model, the study evaluates how geopolitical conflicts influence the interdependencies among these commodities.

## Motivation
Geopolitical events, such as the Russian-Ukrainian war, significantly alter commodity market dynamics. Understanding these changes is critical for improving risk assessment, portfolio management, and strategic decision-making.

## Data
- **Source**: Daily price data from the Chicago Mercantile Exchange.
- **Commodities**: Gold futures, crude oil futures, and corn futures.
- **Timeframe**: 2019-05-02 to 2024-05-02.
- **Division**: Data is divided into pre-war (before February 2022) and since-war periods for separate analyses.

## Methodology

### Data Preprocessing and Detrending
1. **Reshaping Data**:
   - Data was reshaped from long to wide format using `pivot_wider` to align all commodity prices by date.
   - Missing values were filtered out to ensure complete data for all commodities.

2. **Stationarity Testing**:
   - Returns were calculated as the logarithmic differences of prices:  
     \( r_t = \log(P_t) - \log(P_{t-1}) \).
   - Augmented Dickey-Fuller (ADF) tests were performed on returns for each commodity to ensure stationarity.

3. **Autocorrelation and Trend Testing**:
   - Partial Autocorrelation Function (PACF) plots were generated to check for significant lag terms.
   - The Ljung-Box test was conducted to evaluate the presence of autocorrelation in residuals.

4. **Removing Trends**:
   - For commodities with significant autocorrelation, an autoregressive (AR) model was fitted:
     - **Gold**: AR(11) model.
     - **Crude Oil**: AR(4) model.
     - **Corn**: No significant autocorrelation, AR model not required.
   - Residuals from the AR models were used for further analysis to remove trend effects.

### Modeling Process
1. **Univariate GARCH Models**:
   - A GARCH(1,1) model was applied to the residuals of each commodity to capture volatility dynamics.
   - The conditional variance for each series was estimated, assuming a Student’s t-distribution for residuals.

2. **Dynamic Conditional Correlation (DCC)**:
   - Standardized residuals from the GARCH models were input into the DCC-GARCH model.
   - Time-varying conditional correlations between commodities were estimated using:
     \[
     Q_t = (1 - a - b)\bar{Q} + a(z_{t-1}z_{t-1}^\prime) + bQ_{t-1}
     \]
     where \( Q_t \) is the dynamic conditional covariance matrix.

### Structural Breaks
- Bai-Perron tests were applied to detect structural breaks in conditional covariances.
- The analysis identified significant breaks around February 2022, coinciding with the onset of the war.

### Temporal Analysis
- Separate DCC-GARCH models were fitted for the pre-war and since-war periods.
- Changes in unconditional correlations between commodities were analyzed to capture long-term effects.

## Key Findings
- **Temporal Correlations**: Peaks in conditional correlations for all commodity pairs were observed around February 2022.
- **Structural Breaks**: Significant breaks in conditional covariances align with the start of the war.
- **Long-Term Effects**: Unconditional correlations revealed lasting changes, particularly for crude oil & gold and gold & corn.

## Tools and Libraries
- **R**: Primary programming language for analysis.
- **Key Libraries**: `dplyr`, `tidyquant`, `rugarch`, `rmgarch`, `forecast`.

## Repository Contents
- `data/`: Raw and processed datasets.
- `scripts/`: R scripts for data preprocessing, modeling, and visualization.
- `results/`: Output plots, model summaries, and Bai-Perron test results.
- `report/`: Detailed project report.

## Future Directions
- Expanding the analysis to include other commodities such as natural gas for a broader understanding of market dynamics.
- Investigating the effects of other geopolitical or global events on commodity correlations.

## Author
Zhihao Shan  
Columbia Business School  
Master of Science in Financial Economics  

---
For questions or collaborations, reach out via the repository's Issues section.

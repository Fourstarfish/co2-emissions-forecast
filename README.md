# Charting the Carbon Future: CO₂ Emissions Forecasts

A rigorous time-series analysis of global annual CO₂ emissions (1751–2021) using ARIMA and TBATS models to produce short- to medium-term forecasts and compare model performance.

---

## Table of Contents

- [Project Overview](#project-overview)  
- [Dataset](#dataset)  
- [Methods](#methods)  
- [Results](#results)  
- [Discussion & Policy Implications](#discussion--policy-implications)  
- [Limitations & Future Work](#limitations--future-work)  
- [Reproducibility](#reproducibility)  
- [Project Structure](#project-structure)  
- [Contributors](#contributors)  
- [License](#license)  

---

## Project Overview

This study forecasts global annual CO₂ emissions, sourced from Our World in Data (OWID), by fitting two complementary time-series models:  
- **ARIMA(0,1,1) with drift** on a Box–Cox transformed series (λ ≈ 0.0839)  
- **TBATS** (Box–Cox, ARMA(1,0), no seasonal harmonics)

The aim is to evaluate forecast accuracy via out-of-sample testing (2001–2021) and rolling-origin cross-validation.

---

## Dataset

- **Source**: OWID CO₂ and Greenhouse Gas Emissions dataset (`owid-co2-data.csv`)  
- **Series**: Global annual CO₂ emissions (million tonnes), 1751–2021 (271 observations)  
- **Key Transformations**:  
  - Box–Cox λ = 0.084 to stabilize variance  
  - First difference for stationarity (confirmed by ADF and KPSS tests)

---

## Methods

1. **Exploratory Analysis**  
   - Trend visualization and structural break detection  
   - Stationarity tests (ADF, KPSS)  

2. **Model Fitting**  
   - **ARIMA**: `auto.arima()` on Box–Cox transformed, differenced series, fixed seasonal=FALSE  
   - **TBATS**: `tbats()` to allow automated trend and ARMA components  

3. **Forecast Evaluation**  
   - **Hold-out set**: Training up to 2000, test 2001–2021  
   - **Metrics**: RMSE, MAE, MAPE  
   - **Rolling-origin CV**: One-step forecasts across full series  

---

## Results

| Model  | Test RMSE | Test MAE | Test MAPE | CV RMSE |
|--------|-----------|----------|-----------|---------|
| ARIMA  | 2267.8    | 1707.6   | 4.89%     | 327.3   |
| TBATS  | 4329.1    | 4013.9   | 11.71%    | 347.1   |

- **ARIMA** outperformed **TBATS** on both hold-out and CV metrics.  
- Forecast plot shows ARIMA more closely tracking accelerating emissions trends.

---

## Discussion & Policy Implications

- **Model Choice**: Parsimonious ARIMA is more adaptable to the strong upward trend without overfitting.  
- **Policy Relevance**: Reliable emissions forecasts inform climate policy, IPCC assessments, and investment decisions.

---

## Limitations & Future Work

- **Univariate scope**: Excludes exogenous factors (GDP, energy use).  
- **Structural shifts**: Consider regime-switching or ARIMAX extensions.  
- **Hybrid models**: Combine ARIMA residuals with nonlinear learners.  
- **Regional analysis**: Extend to multivariate or panel frameworks.

---

## Reproducibility

1. **Clone the repository**  
   ```bash
   git clone https://github.com/your-username/co2-emissions-forecast.git
   cd co2-emissions-forecast
   ```

2. **Install R packages**  
   ```r
   install.packages(c("forecast", "tseries", "zoo", "ggplot2", "tibble"))
   ```

3. **Render the report**  
   ```r
   rmarkdown::render("STA457 Final Project.Rmd")
   ```

---

## Project Structure

```
├── STA457 Final Project.pdf     # Final report  
├── STA457 Final Project.Rmd     # R Markdown source (screenshots in appendix)  
├── owid-co2-data.csv            # Raw data  
├── figures/                     # Plots used in report  
└── README.md                    # This file  
```

---

## Contributors

- **Mohammad Danish Malik** – Data analysis, modeling, interpretation, and writing  

---

## License

Released under the MIT License. See [LICENSE](LICENSE) for details.

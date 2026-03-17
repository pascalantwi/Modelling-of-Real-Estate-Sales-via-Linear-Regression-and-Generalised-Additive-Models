

This repository contains the code and documentation for a comparative study of linear regression and generalized additive models (GAMs) applied to residential real estate price prediction. The project was completed as part of a final examination and evaluates the predictive performance of these two approaches using a dataset of 522 property transactions.

## Overview

Accurate real estate valuation is critical for market efficiency, mortgage lending, and investment decisions. Traditional hedonic pricing models rely on linear regression, which may fail to capture the complex, non‑linear relationships inherent in housing markets. This study systematically compares:

- **Multiple linear regression** (with diagnostic checks and transformations)
- **Generalized additive models** (GAMs) that allow smooth, non‑linear functions of predictors

Using k‑fold cross‑validation, we assess model fit, predictive accuracy, and stability. The results show that GAMs generally outperform linear models, especially for key predictors like square footage, while linear models retain value for interpretability.

## Dataset

The data consist of 522 residential real estate transactions recorded in a mid‑western U.S. urban area during 2002 (source: Kutner et al., 2005). The variables include:

| Variable             | Description                                      |
|----------------------|--------------------------------------------------|
| `Sales price`        | Sale price (response variable)                   |
| `Finished square ft` | Finished square footage                          |
| `Number of bedrooms` | Count of bedrooms                                |
| `Number of bathrooms`| Count of bathrooms                               |
| `Air conditioning`   | Presence of air conditioning (yes/no)            |
| `Garage size`        | Garage capacity (number of cars)                 |
| `Pool`               | Presence of a pool (yes/no)                      |
| `Year Built`         | Construction year (categorised into periods)     |
| `Quality`            | Construction quality (high/medium/low)           |
| `Style`              | Architectural style (coded as 1‑3, 4‑6, 7‑11)    |
| `Lot size`           | Lot size in square feet                          |
| `Adjacent to highway`| Adjacent to highway (yes/no)                     |

## Methodology

### Linear Regression
- **Model**: \( y = X\beta + \epsilon \)
- **Assumptions**: normality of residuals, homoscedasticity, independence, linearity.
- **Diagnostics**: 
  - Shapiro‑Wilk test for normality
  - Breusch‑Pagan test for heteroscedasticity
  - Variance Inflation Factor (VIF) for multicollinearity
  - Cook’s distance for influential observations
- **Remedial measures**: logarithmic and Box‑Cox transformations.

### Generalized Additive Models (GAMs)
- **Model**: \( g(\mathbb{E}[Y]) = \beta_0 + f_1(X_1) + \dots + f_p(X_p) \)
- Smooth functions \( f_j \) are estimated using penalised regression splines.
- Implemented with the `mgcv` package in R.

### Model Evaluation
- **k‑fold cross‑validation** (k = 2) for robust performance estimates.
- **Metrics**: Root Mean Squared Error (RMSE), \( R^2 \), AIC, BIC.
- Predictor importance assessed by the increase in RMSE when a variable is omitted.

All analyses were performed in R. The code is organised into scripts that replicate the entire workflow: data loading, exploratory analysis, model fitting, diagnostics, and cross‑validation.

## Key Findings

- The linear model explained 82.9% of the variance but violated key assumptions (non‑normality: Shapiro‑Wilk \( p < 0.001 \); heteroscedasticity: Breusch‑Pagan \( p < 0.001 \)).
- Log transformation improved fit (\( R^2 = 0.834 \)) and reduced RMSE, but residual diagnostics still showed mild deviations from normality and constant variance.
- GAMs achieved superior predictive accuracy, especially for square footage (RMSE = 0.0194 vs. 0.0206 in the log‑linear model) and demonstrated greater stability across cross‑validation folds (SD of \( R^2 = 0.015 \) vs. 0.052 for linear models).
- The most influential predictors were **finished square footage**, **construction quality**, and **number of bathrooms**.
- GAMs are recommended when predictive accuracy is paramount; linear models remain useful for exploratory analysis and applications where interpretability is essential.



## References

- Rosen, S. (1974). Hedonic prices and implicit markets: Product differentiation in pure competition. *Journal of Political Economy*, 82(1), 34‑55.
- Wood, S. N. (2017). *Generalized Additive Models: An Introduction with R*. Chapman & Hall/CRC.
- Kutner, M. H., Nachtsheim, C. J., Neter, J., & Li, W. (2005). *Applied Linear Statistical Models*. McGraw‑Hill.
- Hastie, T., & Tibshirani, R. (1986). Generalized additive models. *Statistical Science*, 1(3), 297‑310.


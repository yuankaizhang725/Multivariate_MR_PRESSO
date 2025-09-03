# Multivariate MR-PRESSO

An R implementation extending the MR-PRESSO (Mendelian Randomization Pleiotropy RESidual Sum and Outlier) method to handle multiple outcomes simultaneously in Mendelian Randomization analyses.

## Overview

This package provides functions to:
- Detect outliers across multiple outcomes using Mahalanobis distances
- Perform distortion tests to assess bias from pleiotropy
- Generate outlier-corrected causal estimates
- Create comprehensive diagnostic plots

## Key Features

- **Multivariate outlier detection**: Uses Mahalanobis distances instead of univariate residuals
- **Global and individual SNP testing**: Comprehensive outlier identification
- **Bias correction**: Provides both raw and outlier-corrected estimates
- **Rich visualization**: Forest plots, residual diagnostics, and Q-Q plots

## Functions

### `mr_presso_multivariate()`
Main function for multivariate MR-PRESSO analysis.

**Parameters:**
- `BetaOutcome`: Column names for outcome betas
- `BetaExposure`: Column names for exposure betas  
- `SdOutcome`: Column names for outcome standard errors
- `SdExposure`: Column names for exposure standard errors
- `data`: Data frame with MR summary statistics
- `OUTLIERtest`: Perform outlier detection (default: FALSE)
- `DISTORTIONtest`: Perform distortion test (default: FALSE)
- `SignifThreshold`: P-value threshold for outliers (default: 0.05)
- `NbDistribution`: Simulations for empirical p-values (default: 1000)

### `plot_mr_presso_multivariate()`
Generate diagnostic plots for results visualization.

## Usage Example

```r
# Load your MR data
data <- read.csv("your_mr_data.csv")

# Run multivariate MR-PRESSO
results <- mr_presso_multivariate(
  BetaOutcome = c("beta_outcome1", "beta_outcome2"),
  BetaExposure = c("beta_exposure1", "beta_exposure2"), 
  SdOutcome = c("se_outcome1", "se_outcome2"),
  SdExposure = c("se_exposure1", "se_exposure2"),
  data = data,
  OUTLIERtest = TRUE,
  DISTORTIONtest = TRUE
)

# Generate diagnostic plots
plots <- plot_mr_presso_multivariate(results, data, 
                                    BetaOutcome = c("beta_outcome1", "beta_outcome2"),
                                    BetaExposure = c("beta_exposure1", "beta_exposure2"),
                                    plot_type = "all")

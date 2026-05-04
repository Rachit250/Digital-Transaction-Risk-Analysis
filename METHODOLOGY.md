# 📐 Statistical Methodology & Technical Approach

## Overview

This document outlines the statistical techniques, methods, and mathematical foundations used throughout the 6-unit Digital Transaction Risk Analysis project. It serves as a reference guide for practitioners and as a foundation for statistical event presentations.

---

## Unit 1: Data Cleaning & Feature Engineering

### 1.1 Data Quality Assessment

**Missing Value Detection**:
- Null count analysis: $\text{missing} = \sum_{i=1}^{n} \text{isNull}(x_i)$
- Missing percentage: $\text{pct\_missing} = \frac{\text{missing}}{n} \times 100$

**Duplicate Detection**:
- Row-level comparison for exact duplicates
- Hash-based deduplication for efficiency

### 1.2 Outlier Detection: IQR Method

The Interquartile Range (IQR) method identifies extreme values:

$$Q_1 = \text{25th percentile}$$
$$Q_3 = \text{75th percentile}$$
$$\text{IQR} = Q_3 - Q_1$$
$$\text{Lower Bound} = Q_1 - 1.5 \times \text{IQR}$$
$$\text{Upper Bound} = Q_3 + 1.5 \times \text{IQR}$$

**Outlier Flag**: $\text{outlier} = 1$ if $x < \text{Lower Bound}$ or $x > \text{Upper Bound}$

### 1.3 Feature Scaling Methods

**Z-Score Standardization** (Standardization):
$$z = \frac{x - \mu}{\sigma}$$
- Transforms to $\mathcal{N}(0, 1)$ distribution
- Preserves relationships between features
- Essential for algorithms sensitive to scale (SVM, KNN, Linear Regression)

**Min-Max Normalization** (Rescaling):
$$x_{\text{norm}} = \frac{x - x_{\min}}{x_{\max} - x_{\min}}$$
- Bounds features to $[0, 1]$
- Useful for neural networks and tree-based ensemble methods

**Winsorization** (Capping):
$$x_{\text{capped}} = \max(\text{Lower Bound}, \min(x, \text{Upper Bound}))$$
- Retains outlier rows while capping extreme values
- Reduces impact of extreme values without loss of information

### 1.4 Temporal Feature Engineering

**Transaction Hour**: Extract hour of day (0-23)
- **Rationale**: Fraud patterns differ by time of day

**Day of Week**: Categorical encoding (Monday-Sunday)
- **Rationale**: Weekend vs. weekday behavior differences

**Weekend Flag**: Binary indicator
$$\text{is\_weekend} = \begin{cases} 1 & \text{if day} \in \{\text{Sat, Sun}\} \\ 0 & \text{otherwise} \end{cases}$$

**Transaction Month**: Monthly seasonality capture

---

## Unit 2: Exploratory Data Analysis

### 2.1 Descriptive Statistics

**Central Tendency**:
- Mean: $\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i$
- Median: Middle value when data sorted
- Mode: Most frequently occurring value

**Dispersion**:
- Variance: $\sigma^2 = \frac{1}{n}\sum_{i=1}^{n} (x_i - \bar{x})^2$
- Standard Deviation: $\sigma = \sqrt{\sigma^2}$
- IQR: $Q_3 - Q_1$ (spread of middle 50%)
- Range: $x_{\max} - x_{\min}$

**Skewness**: $\gamma = E\left[\left(\frac{x-\mu}{\sigma}\right)^3\right]$
- Measures asymmetry of distribution
- $\gamma = 0$: Symmetric
- $\gamma < 0$: Left-skewed
- $\gamma > 0$: Right-skewed

**Kurtosis**: $k = E\left[\left(\frac{x-\mu}{\sigma}\right)^4\right] - 3$
- Measures tail heaviness
- $k = 0$: Normal distribution
- $k > 0$: Heavy tails (leptokurtic)
- $k < 0$: Light tails (platykurtic)

### 2.2 Correlation Analysis

**Pearson Correlation Coefficient**:
$$r = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y} = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum(x_i-\bar{x})^2}\sqrt{\sum(y_i-\bar{y})^2}}$$

- Range: $-1 \leq r \leq 1$
- $r \approx 1$: Strong positive correlation
- $r \approx 0$: No linear correlation
- $r \approx -1$: Strong negative correlation

**Spearman Rank Correlation** (for non-linear relationships):
$$\rho = 1 - \frac{6\sum d_i^2}{n(n^2-1)}$$
where $d_i$ = difference in ranks

### 2.3 Distribution Analysis

**Histogram Binning**:
- Sturges' Rule: $k = \lceil \log_2(n) + 1 \rceil$
- Freedman-Diaconis: $\text{width} = 2 \cdot \text{IQR} \cdot n^{-1/3}$

**Kernel Density Estimation (KDE)**:
$$f(x) = \frac{1}{n h}\sum_{i=1}^{n} K\left(\frac{x - x_i}{h}\right)$$
where $K$ = kernel function, $h$ = bandwidth

---

## Unit 3: Statistical Hypothesis Testing

### 3.1 Chi-Square Test of Independence

For categorical variables (fraud vs. day of week):

$$\chi^2 = \sum_{i,j} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}$$

where:
- $O_{ij}$ = observed frequency in cell $(i,j)$
- $E_{ij}$ = expected frequency under independence
- $E_{ij} = \frac{n_{i\cdot} \cdot n_{\cdot j}}{n}$

**Null Hypothesis** ($H_0$): Fraud and day of week are independent  
**Alternative Hypothesis** ($H_1$): Fraud and day of week are dependent  
**Significance Level**: $\alpha = 0.05$  
**Decision**: Reject $H_0$ if $\chi^2 > \chi^2_{\alpha, df}$ or $p\text{-value} < \alpha$

### 3.2 Two-Sample t-Test

For comparing fraud rates between groups:

$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$$

where $s^2$ = sample variance, $n$ = sample size

**Assumptions**:
1. Independence of observations
2. Normality (or large sample size $n > 30$)
3. Equal variances (use Welch's t-test if violated)

**Degrees of Freedom** (Welch):
$$df = \frac{\left(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}\right)^2}{\frac{s_1^4}{n_1^2(n_1-1)} + \frac{s_2^4}{n_2^2(n_2-1)}}$$

### 3.3 Effect Size: Cohen's d

Standardized difference between means:

$$d = \frac{\bar{x}_1 - \bar{x}_2}{s_{\text{pooled}}}$$

where $s_{\text{pooled}} = \sqrt{\frac{(n_1-1)s_1^2 + (n_2-1)s_2^2}{n_1 + n_2 - 2}}$

**Interpretation**:
- $|d| < 0.2$: Small effect
- $0.2 \leq |d| < 0.8$: Medium effect
- $|d| \geq 0.8$: Large effect

---

## Unit 4: Predictive Modeling

### 4.1 Class Imbalance: SMOTE

Synthetic Minority Oversampling Technique creates synthetic samples:

$$\text{synthetic} = x_i + \lambda \cdot (x_{nn} - x_i)$$

where:
- $x_i$ = minority class sample
- $x_{nn}$ = nearest neighbor in feature space
- $\lambda$ = random value in $[0, 1]$

**Benefits**: Improved minority class recall without data duplication

### 4.2 Random Forest

**Ensemble Method**: Combines $B$ decision trees

$$\hat{f}_{\text{RF}}(x) = \frac{1}{B}\sum_{b=1}^{B} T_b(x)$$

**Feature Importance** (Mean Decrease in Impurity):
$$\text{Importance}_j = \sum_{nodes} p(node) \cdot \Delta \text{Impurity}_j$$

where impurity = Gini or entropy

### 4.3 Model Evaluation Metrics

**Confusion Matrix**:
|  | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actual Positive** | TP | FN |
| **Actual Negative** | FP | TN |

**Accuracy**:
$$\text{Acc} = \frac{TP + TN}{TP + TN + FP + FN}$$
- Overall correctness; problematic with imbalanced data

**Precision**:
$$\text{Prec} = \frac{TP}{TP + FP}$$
- "Of predicted positives, how many are correct?"
- Important when false positives are costly

**Recall (Sensitivity)**:
$$\text{Rec} = \frac{TP}{TP + FN}$$
- "Of actual positives, how many did we catch?"
- Important when false negatives are costly

**F1-Score** (Harmonic Mean):
$$F_1 = 2 \cdot \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$
- Balanced metric for imbalanced classification

**Area Under ROC Curve (AUC-ROC)**:
- Plots TPR vs. FPR across thresholds
- AUC = 0.5: Random classifier
- AUC = 1.0: Perfect classifier
- Threshold-independent; ideal for imbalanced data

**ROC Curve**:
$$\text{TPR} = \frac{TP}{TP + FN}, \quad \text{FPR} = \frac{FP}{FP + TN}$$

### 4.4 Cross-Validation

**Stratified k-Fold** (preserves class distribution):

$$\text{CV Error} = \frac{1}{k}\sum_{i=1}^{k} \text{Error}_i$$

For imbalanced data, stratification ensures each fold has similar fraud rate.

---

## Unit 5: Dimensionality Reduction - PCA

### 5.1 Principal Component Analysis (PCA)

**Objective**: Find orthogonal directions of maximum variance

**Step 1** - Standardize data:
$$X_{\text{std}} = \frac{X - \mu}{\sigma}$$

**Step 2** - Compute covariance matrix:
$$\text{Cov}(X) = \frac{1}{n-1}X^T X$$

**Step 3** - Eigendecomposition:
$$\text{Cov}(X) \cdot v_j = \lambda_j \cdot v_j$$

where $v_j$ = eigenvector (principal component), $\lambda_j$ = eigenvalue (variance)

**Step 4** - Project data:
$$X_{\text{PCA}} = X_{\text{std}} \cdot V_k$$

where $V_k$ = matrix of first $k$ eigenvectors

### 5.2 Variance Explained

**Individual PC**:
$$\text{Var}_j = \frac{\lambda_j}{\sum_{i=1}^{p} \lambda_i}$$

**Cumulative (Scree Plot)**:
$$\text{Cum Var}_k = \frac{\sum_{j=1}^{k} \lambda_j}{\sum_{i=1}^{p} \lambda_i}$$

- Determine $k$ where cumulative variance ≥ 95% (typical threshold)

### 5.3 t-SNE (t-Distributed Stochastic Neighbor Embedding)

Non-linear dimensionality reduction for visualization:

**Pairwise similarity in original space**:
$$p_{j|i} = \frac{\exp(-\|x_i - x_j\|^2 / 2\sigma_i^2)}{\sum_{k \neq i} \exp(-\|x_i - x_k\|^2 / 2\sigma_i^2)}$$

**Pairwise similarity in reduced space** (using Student's t-distribution):
$$q_{ij} = \frac{(1 + \|y_i - y_j\|^2)^{-1}}{\sum_{k \neq l} (1 + \|y_k - y_l\|^2)^{-1}}$$

**Minimize KL divergence**:
$$C = \sum_i KL(P_i \| Q_i) = \sum_i \sum_j p_{ij} \log \frac{p_{ij}}{q_{ij}}$$

---

## Unit 6: Time Series Analysis

### 6.1 ARIMA(p,d,q) Model

**AR (AutoRegressive) component**:
$$y_t = c + \phi_1 y_{t-1} + \phi_2 y_{t-2} + \cdots + \phi_p y_{t-p} + \epsilon_t$$

**I (Integrated) component**: Apply $d$ differencing steps
$$\Delta y_t = y_t - y_{t-1}$$

**MA (Moving Average) component**:
$$y_t = c + \epsilon_t + \theta_1 \epsilon_{t-1} + \theta_2 \epsilon_{t-2} + \cdots + \theta_q \epsilon_{t-q}$$

**Combined ARIMA(p,d,q)**:
$$\phi(B) \Delta^d y_t = \theta(B) \epsilon_t$$

where $B$ = backshift operator, $\phi(B)$ = AR polynomial, $\theta(B)$ = MA polynomial

### 6.2 Model Selection

**ACF (Autocorrelation Function)**:
$$\rho(h) = \frac{\text{Cov}(y_t, y_{t+h})}{\text{Var}(y_t)}$$

**PACF (Partial Autocorrelation Function)**: Correlation excluding intermediate lags

**AIC (Akaike Information Criterion)**:
$$\text{AIC} = 2k + n\ln(\text{RSS}/n)$$
where $k$ = parameters, $n$ = observations, $\text{RSS}$ = residual sum of squares

**NDIFFS/NDIFFS**: Tests for stationarity (Kwiatkowski-Phillips-Schmidt-Shin test)

### 6.3 Forecast Evaluation

**Mean Absolute Percentage Error (MAPE)**:
$$\text{MAPE} = \frac{100}{n}\sum_{t=1}^{n} \left|\frac{y_t - \hat{y}_t}{y_t}\right|$$

**Root Mean Squared Error (RMSE)**:
$$\text{RMSE} = \sqrt{\frac{1}{n}\sum_{t=1}^{n} (y_t - \hat{y}_t)^2}$$

**Ljung-Box Test** (residual autocorrelation):
$$Q = n(n+2)\sum_{h=1}^{m} \frac{r_h^2}{n-h}$$
- Tests if residuals are independently distributed
- Under $H_0$: $Q \sim \chi^2_m$

---

## Summary of Key Assumptions & Limitations

| Technique | Key Assumption | Robustness |
|-----------|---|---|
| **t-test** | Normality, equal variance | Good for $n > 30$ |
| **Chi-square** | Expected frequency > 5 | Good for categorical data |
| **Linear Regression** | Linearity, homoscedasticity | Affected by outliers |
| **Random Forest** | Tree independence | Robust to non-linearity |
| **PCA** | Linearity, variance → importance | Poor for non-linear patterns |
| **ARIMA** | Stationarity (after differencing) | Requires time-ordered data |

---

## References & Further Reading

1. **Statistical Testing**: Shapiro, W. (1964). An Analysis of Variance Test for Normality
2. **Classification Metrics**: Fawcett, T. (2006). An introduction to ROC analysis
3. **Dimensionality Reduction**: Maaten & Hinton (2008). Visualizing Data using t-SNE
4. **Time Series**: Box, Jenkins, Reinsel, Ljung (2015). Time Series Analysis: Forecasting and Control
5. **Machine Learning**: Hastie, Tibshirani, Friedman (2009). The Elements of Statistical Learning

---

**Document Version**: 1.0  
**Last Updated**: May 2026  
**Status**: Ready for Statistical Event Presentation ✅

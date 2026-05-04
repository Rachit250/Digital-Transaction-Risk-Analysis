# Digital Transaction Risk Analysis
## A Comprehensive Statistical Analysis Framework for Fraud Detection & Financial Risk Assessment

> **Professional-grade data science project** analyzing transaction risk patterns across the full ML lifecycle — from raw data to actionable insights. Demonstrates statistical rigor, advanced modeling techniques, and production-ready data engineering practices.

---

## Executive Summary

This 6-unit comprehensive analysis covers **1.3M+ digital transactions** with a **0.58% fraud rate** (imbalanced classification). The project demonstrates:

- ✅ **Data Engineering**: Complete cleaning, feature engineering, and preprocessing pipeline
- ✅ **Exploratory Analysis**: Detailed EDA with statistical distributions and temporal patterns  
- ✅ **Statistical Testing**: Hypothesis validation using Chi-square, t-tests, and effect sizes
- ✅ **Predictive Modeling**: Multiple algorithms (RF, XGBoost, Logistic Regression) with SMOTE balancing
- ✅ **Dimensionality Reduction**: PCA & t-SNE for high-dimensional pattern discovery
- ✅ **Time Series Analysis**: ARIMA forecasting & anomaly detection

**Key Finding**: Transaction amount, merchant distance, and temporal features are strong fraud indicators (AUC > 0.92)

---

## Project Objectives

1. **Data Quality Assurance** - Identify and resolve data integrity issues
2. **Pattern Discovery** - Uncover fraud characteristics through statistical analysis
3. **Predictive Modeling** - Build robust models for real-time fraud detection
4. **Risk Segmentation** - Reduce dimensionality to identify risk clusters
5. **Temporal Forecasting** - Predict transaction volume and anomalies

---

## Unit-by-Unit Breakdown

| Unit | Topic | Key Techniques | Deliverables |
|------|-------|----------------|--------------|
| **Unit 1** | Data Cleaning & Feature Engineering | IQR outlier detection, Winsorization, Time-based features | Clean dataset, 27 engineered features |
| **Unit 2** | Exploratory Data Analysis | Distribution analysis, correlation, temporal patterns | 8+ publication-ready visualizations |
| **Unit 3** | Statistical Inference | Chi-square tests, t-tests, effect sizes (Cohen's d) | Validated hypotheses with p-values |
| **Unit 4** | Predictive Modeling | Random Forest, XGBoost, SMOTE balancing, cross-validation | Models with precision/recall trade-offs |
| **Unit 5** | Dimensionality Reduction | PCA (95% variance), t-SNE visualization | 2D & 3D projections for interpretation |
| **Unit 6** | Time Series Analysis | ARIMA(1,0,1), trend decomposition | Forecasts with confidence intervals |

---

## Quick Start

### Option 1: Run Locally (Recommended)
```bash
# Clone repository
git clone https://github.com/Rachit250/Digital-Transaction-Risk-Analysis.git
cd Digital-Transaction-Risk-Analysis

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

### Option 2: Cloud Execution (No Setup Required)
- **JupyterBinder**: [![Launch Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Rachit250/Digital-Transaction-Risk-Analysis/main?urlpath=lab/tree/Unit1_Data_Cleaning.ipynb)
- **Google Colab**: Open any `.ipynb` file → Click "Open in Colab"

---

## File Structure
```
Digital-Transaction-Risk-Analysis/
├── fraudTrain.csv                      # 1.3M transaction records with fraud labels
├── Unit1_Data_Cleaning.ipynb           # ✨ Data preprocessing & feature engineering
├── Unit2_Descriptive_Analysis.ipynb    # 📊 EDA with statistical summaries
├── Unit3_Inferential_Testing.ipynb     # 🔬 Hypothesis testing & validation
├── Unit4_Predictive_Modeling.ipynb     # 🤖 ML models with evaluation
├── Unit5_Dimensionality_Reduction.ipynb # 📉 PCA & visualization
├── Unit6_Time_Series_Analysis.ipynb    # ⏱️ ARIMA & trend analysis
├── requirements.txt                    # Python dependencies
├── runtime.txt                         # Python version specification
└── README.md                           # This file
```

---

## Technologies & Libraries

**Core Stack**:
- ![Python](https://img.shields.io/badge/Python-3.8+-3776ab?logo=python&logoColor=white)
- ![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-f37726?logo=jupyter)
- ![Pandas](https://img.shields.io/badge/Pandas-2.2.2-150458?logo=pandas)
- ![NumPy](https://img.shields.io/badge/NumPy-1.26.4-013243?logo=numpy)

**Analysis & Modeling**:
- ![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.4.2-f7931e?logo=scikit-learn)
- ![Statsmodels](https://img.shields.io/badge/Statsmodels-0.14.2-Time%20Series-1f77b4)
- ![Imbalanced-learn](https://img.shields.io/badge/Imbalanced--learn-SMOTE%20Balancing-007acc)

**Visualization**:
- ![Matplotlib](https://img.shields.io/badge/Matplotlib-3.8.4-FFD43B)
- ![Seaborn](https://img.shields.io/badge/Seaborn-0.13.2-Data%20Viz-449999)
- ![Plotly](https://img.shields.io/badge/Plotly-5.22.0-Interactive-3F51B5)

---

## Dataset Overview

**Size**: 1,296,675 transactions  
**Features**: 23 original attributes  
**Target**: Binary fraud classification (0.58% positive class)  
**Time Period**: 2019 transaction data  
**Geography**: USA (multi-state coverage)  

**Key Variables**:
- Transaction metadata (date, time, merchant)
- Cardholder demographics (location, age)
- Transaction details (amount, category)
- Spatial features (merchant location vs cardholder)

---

## Learning Outcomes

By studying this project, you'll understand:

✔️ **End-to-end ML workflows** - From raw data to deployed model  
✔️ **Statistical fundamentals** - Hypothesis testing, effect sizes, p-values  
✔️ **Data engineering best practices** - Cleaning, validation, feature engineering  
✔️ **Handling imbalanced data** - SMOTE, class weights, evaluation metrics  
✔️ **Model selection** - Trade-offs between interpretability and performance  
✔️ **Time series forecasting** - ARIMA, trend decomposition, seasonality  
✔️ **Dimensionality reduction** - PCA interpretation and visualization  

---

## Performance Highlights

- **Random Forest**: Precision 0.97, Recall 0.85, AUC-ROC 0.94
- **XGBoost**: Precision 0.96, Recall 0.88, AUC-ROC 0.95  
- **Dimensionality**: 2 PCs capture 78% variance; 5 PCs capture 91%
- **Time Series**: ARIMA forecasts within 5% MAPE of actual values

---

## Key Findings

1. **Temporal Risk**: High fraud rate during late-night hours (11 PM - 3 AM)
2. **Geographic Anomalies**: Fraud spikes when merchant distance > 100 miles
3. **Amount Behavior**: Large transactions ($200+) with unusual patterns flagged
4. **Weekend Effect**: Marginally higher fraud on weekends (0.62% vs 0.57%)
5. **Feature Importance**: Amount, merchant location, and time are top 3 predictors

---

## Usage Examples

### Run a Single Unit
```python
# In Jupyter, simply open and execute any Unit notebook sequentially
```

### Extract Key Statistics
```python
# After running Unit 2, access summary statistics:
df.describe()  # Descriptive statistics
df.corr()      # Correlation matrix
```

### Make Predictions
```python
# After training in Unit 4:
from sklearn.ensemble import RandomForestClassifier
predictions = rf_model.predict(X_test)
probabilities = rf_model.predict_proba(X_test)
```

---

## Contributing

Improvements welcome! Please feel free to:
- Report issues in data processing or visualizations
- Suggest additional statistical tests
- Propose new feature engineering approaches
- Improve documentation and comments

---

## Support & Questions

For questions about methodology or implementation:
1. Review the inline code comments in each notebook
2. Check the detailed docstrings in Unit headers
3. Refer to technique citations in markdown cells
4. Submit issues for bugs or clarifications

---

## 📜 License & Attribution

**Original Project**: Rachit Sharma and Shaad Ashraf
**Enhanced for Professional Presentation**: May 2026

This project is provided for educational purposes. The fraudTrain.csv dataset is used with appropriate attribution to the original source.

---

## 🏆 Recommended for

- **Graduate-level ML/Statistics courses**
- **Data science portfolio projects**
- **Risk management & financial services analytics**
- **Statistical event presentations**
- **Interview preparation & case studies**

---

**Status**: Production-Ready ✅  
**Last Updated**: May 2026

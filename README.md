# Quantitative Macro-Credit Risk Modeling

## Project Highlights

✔ Integrated Lending Club and FRED macroeconomic data

✔ Implemented Point-in-Time joins to eliminate data leakage

✔ Developed Hidden Markov Model regime detection framework

✔ Built nested XGBoost credit risk models

✔ Improved ROC-AUC from 0.683 → 0.715

✔ Improved calibration quality by 73%

✔ Designed macroeconomic stress-testing framework

✔ Demonstrated state-dependent credit default behavior

---

## Overview

Traditional credit risk models often assume that the relationship between borrower characteristics and default risk remains constant over time. However, major economic disruptions such as the Global Financial Crisis (2008) and the COVID-19 pandemic have demonstrated that borrower behavior is strongly influenced by changing macroeconomic conditions.

This project develops a **Regime-Dependent Credit Risk Modeling Framework** that integrates:

* Borrower-specific characteristics
* Macroeconomic indicators
* Latent economic regimes

The objective is to determine whether incorporating macroeconomic conditions and hidden market regimes improves the prediction of borrower default probabilities compared to traditional borrower-only credit risk models.

---

## Research Questions

This study addresses the following questions:

1. Does incorporating macroeconomic information improve Probability of Default (PD) prediction?
2. Do latent economic regimes provide additional predictive power beyond observable macroeconomic variables?
3. Which regime-detection approach best captures meaningful economic states?
4. Can regime-aware models improve model calibration and stability across economic cycles?
5. How do credit risk models behave under simulated economic stress scenarios?

---

## Methodology

### Data Sources

#### Lending Club Loan Data

Borrower-level information including:

* Loan amount
* Interest rate
* Debt-to-Income Ratio (DTI)
* FICO score
* Revolving utilization
* Annual income
* Loan status (default/non-default)

#### FRED Macroeconomic Data

Macroeconomic variables obtained from the Federal Reserve Economic Data (FRED):

* Unemployment Rate
* Credit Spread
* Yield Curve
* Consumer Price Index (CPI)
* Industrial Production Growth
* Federal Funds Rate
* GDP-related indicators

---

### Data Engineering

The project employs a **Point-in-Time Join Framework** to merge loan records with macroeconomic information available at the time of loan issuance.

Key features:

* Monthly alignment of macroeconomic variables
* One-period lagging of macro variables
* Prevention of look-ahead bias
* Time-series aware train/test split

---

### Regime Detection

Latent economic states are identified using:

#### Hidden Markov Model (HMM)

* Gaussian emissions
* Maximum Likelihood Estimation
* Expectation-Maximization (EM) algorithm

Detected regimes:

1. Expansion / Normal Regime
2. Stress / Recovery Regime

#### Additional Methods Explored

* Gaussian Mixture Models (GMM)
* K-Means Clustering

---

### Predictive Modeling

Credit default prediction is performed using **XGBoost**.

Three nested models are developed:

#### Model 1: Traditional Credit Risk Model

Features:

* Borrower characteristics only

#### Model 2: Macro-Augmented Model

Features:

* Borrower characteristics
* Macroeconomic variables

#### Model 3: Regime-Aware Model

Features:

* Borrower characteristics
* Macroeconomic variables
* HMM regime labels

---

## Model Evaluation

Models are evaluated using:

* ROC-AUC
* Precision-Recall AUC (PR-AUC)
* Brier Score
* Calibration Curves

Additionally:

* Out-of-sample testing
* Economic stress-testing simulations

---

## Results

### Hidden Markov Regime Detection

The HMM successfully identified economically meaningful latent states:

| Regime    | Characteristics                                                         |
| --------- | ----------------------------------------------------------------------- |
| Expansion | Lower unemployment, tighter credit spreads, stronger economic activity  |
| Stress    | Higher unemployment, wider credit spreads, weaker industrial production |

The detected stress regime broadly aligned with post-2008 crisis conditions.

---

### Model Performance

| Model                      | ROC-AUC    | PR-AUC     | Brier Score |
| -------------------------- | ---------- | ---------- | ----------- |
| Borrower Features Only     | 0.6830     | 0.0268     | 0.2179      |
| Borrower + Macro Variables | 0.7050     | 0.0382     | 0.0632      |
| Borrower + Macro + Regime  | **0.7150** | **0.0421** | **0.0575**  |

### Key Findings

* Macroeconomic variables significantly improve credit risk prediction.
* Latent economic regimes contain additional predictive information.
* Regime-aware models produce superior calibration.
* Credit risk is inherently state-dependent.
* Traditional static models underestimate risk during stressed economic environments.

---

## Stress Testing Framework

The project includes scenario analysis by manually shifting macroeconomic variables toward crisis levels.

Examples:

* Global Financial Crisis (2008)
* Severe unemployment shock
* Credit spread widening

This allows assessment of:

* Probability of Default migration
* Model stability
* Sensitivity to macroeconomic shocks

---

## Repository Structure

```text
quantitative-macro-credit-risk-modeling/
│
├── README.md
├── requirements.txt
├── LICENSE
│
├── notebooks/
│   └── Quantitative_Macro_Credit_Risk_Modeling.ipynb
│
├── figures/
│   ├── workflow.png
│   ├── hmm_regimes.png
│   ├── roc_curve.png
│   ├── precision_recall_curve.png
│   ├── calibration_curve.png
│   └── feature_importance.png
│
├── report/
│   └── MSc_Capstone_Project_Final_GP_14074.pdf
│
└── data/
    └── sample_data_description.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/quantitative-macro-credit-risk-modeling.git

cd quantitative-macro-credit-risk-modeling
```

Create a virtual environment:

```bash
python -m venv venv

source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Required Libraries

```python
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
hmmlearn
fredapi
scipy
statsmodels
```

Install manually if needed:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost hmmlearn fredapi scipy statsmodels
```

---

## Running the Project

Open the notebook:

```bash
jupyter notebook
```

Run:

```text
Quantitative_Macro_Credit_Risk_modeling.ipynb
```

The notebook performs:

1. Data loading
2. Feature engineering
3. Point-in-time data integration
4. Regime detection
5. Model training
6. Performance evaluation
7. Stress testing
8. Visualization

---

## Future Enhancements

Potential extensions include:

* Long Short-Term Memory (LSTM) regime detection
* Transformer-based sequence models
* SHAP explainability analysis
* Corporate bond default prediction
* Mortgage credit risk applications
* Cross-country validation studies

---

## Business Impact

Traditional credit scoring models rely primarily on borrower characteristics and often assume stable economic conditions.

This research demonstrates that incorporating macroeconomic conditions and latent economic regimes can materially improve default prediction performance.

### Benefits for Banks

- Better Probability of Default estimation
- Improved capital allocation
- Enhanced Basel-compliant stress testing
- More robust Expected Credit Loss (ECL) calculations
- Improved portfolio risk monitoring

### Benefits for Fintech Lenders

- Dynamic credit scoring during economic shifts
- Earlier detection of deteriorating borrower quality
- Improved pricing of credit products
- Reduced unexpected default losses
- More resilient lending decisions during recessions

### Strategic Insight

The findings suggest that credit risk is fundamentally state-dependent. Borrowers with similar characteristics may exhibit significantly different default behavior depending on prevailing macroeconomic conditions.

Regime-aware machine learning models therefore provide a practical pathway toward next-generation credit risk management systems.

---

## Authors

### Wickliff Siriga Ogari

MSc Financial Engineering Candidate
WorldQuant University

---

## Citation

If you use this work in your research, please cite:

```bibtex
@misc{ogari2026macrocreditrisk,
  title={Quantitative Macro-Credit Risk Modeling},
  author={Ogari, Wickliff Siriga},
  year={2026},
  note={WorldQuant University Capstone Project}
}
```

---

## License

This project is released under the MIT License.

Feel free to fork, modify, and build upon this work for educational and research purposes.

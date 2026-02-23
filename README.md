# 🧵 SignalWeave  
### A Weakly Supervised, Interpretable AML Risk Scoring Framework

> Weaving regulatory intelligence and behavioral signals into a scalable, transparent fraud detection system.
![SignalWeave Architecture](imgs/overall_workflow.png)
---

## 📌 Overview

SignalWeave is a data-centric Anti–Money Laundering (AML) framework designed to detect suspicious financial behavior in partially labeled or unlabeled datasets.

Traditional AML systems rely heavily on:
- Historical SAR-based labels
- Static rule engines
- High false positive alerting
- Limited interpretability in ML models

SignalWeave addresses these challenges by combining:

- 🧠 Regulatory-informed feature engineering  
- 🏷 Weak supervision using Snorkel  
- 🌲 Gradient-boosted decision trees (XGBoost / CatBoost)  
- 🔍 SHAP-based explainability  

The result is a probabilistic AML risk score that balances detection performance with regulatory transparency.

---

## 🎯 Objectives

SignalWeave was built to:

- Reduce reliance on fully labeled fraud datasets  
- Encode regulatory knowledge directly into model supervision  
- Detect emerging suspicious behavioral patterns  
- Maintain explainability for compliance and audit review  
- Provide a modular AML experimentation framework  

---

## 🧠 Core Philosophy: Data-Centric AI

Instead of focusing only on model complexity, SignalWeave prioritizes improving supervision quality.

> Better labels → Better supervision → Better models

Weak supervision enables expert heuristics and regulatory signals to be transformed into probabilistic training labels before downstream modeling.

This allows:
- Scalable domain knowledge integration  
- Reduced manual labeling burden  
- Discovery of hidden fraud patterns  

---

## 🏗 System Architecture

## Snorkel AI
Snorkel AI originated as an open-source research project in 2015 at the Stanford AI Lab. Snorkel is designed to address data bottlenecks through programmatic labelling.
Snorkel uses Labelling Functions (LFs) to assign probabilistic weak labels to unlabelled data. Through conflict and agreement of the LFs the model is able to learn which LFs are more trustworthy.
The result is a weakly labelled dataset that is used to expand the training set.
Snorkel AI has been used by a variety of Fortune 500 companies & government agencies.

If Snorkel is not already installed, you can install it using: `pip install snorkel`

Link to the website: https://www.snorkel.org/ 

## SHAP (SHapley Additive exPlanations)
SHAP is an open-source explainability framework grounded in cooperative
game theory. It assigns each feature a contribution value for an
individual prediction, allowing complex machine learning models to be
interpreted in a transparent and consistent manner.

In SignalWeave, SHAP is used to explain the outputs of gradient-boosted
tree models (XGBoost / CatBoost) by quantifying how each engineered AML
feature increases or decreases a customer's risk score.

SHAP enables both global and local interpretability. Globally, it
identifies which behavioral indicators most influence model decisions
across the portfolio. Locally, it provides case-level explanations that
support investigative review, audit defensibility, and regulatory
transparency.

If SHAP is not already installed, you can install it using: `pip install shap`

Link to the documentation: https://shap.readthedocs.io/

## Business Problems 
The fraud data provided to us faces a serious data bottleneck problem. In order to train a stable downstream model, the training dataset must be expanded. However, hand labelling is time-consuming and costly. Our approach addresses this by using Snorkel, where domain knowledge was directly encoded into Labelling Functions (LFs).

The second business problem was ensuring model interpretability, as transparency is crucial for understanding why customers were flagged for fraud. This was addressed by using XGBoost in combination with SHAP values. XGBoost allowed us to capture complex, non-linear patterns in fraud detection, while SHAP provided a transparent, per-customer explanation for each fraud prediction.

## Tradeoffs & Future Recommendations
Our approach binarized the weak labels into 0 and 1 using a threshold of 0.5. This means that weak labels with scores of 0.55 and 0.95 are treated the same, which may reduce the probabilistic signal produced by Snorkel. However, this was partially mitigated because our Labelling Functions (LFs) were highly precise, and the majority of the weak labels generated were strongly polarized.

In future work, we would aim to repeat the same experiment with two key changes. First, we would expand the LFs to be broader and increase their coverage. Second, instead of binarizing the probabilistic labels, we would retain them as continuous values and train a regression model rather than a classification model. The results from this approach could then be compared against the current implementation to evaluate potential performance improvements.

# AML Knowledge Library

## Overview

---

The AML Knowledge Library is a structured, Excel-based reference framework that documents money laundering (ML) indicators and links them directly to implemented model features.

The library is designed to:
- Provide traceability between AML risk indicators and engineered features  
- Support model transparency and explainability  
- Assist investigative and analytical interpretation of model outputs  
- Demonstrate structured alignment with authoritative AML guidance  

The focus is on clarity, usability, and defensibility.


## Workbook Structure

The Excel workbook contains two sheets:

1. **AML Knowledge**  
2. **High Risk Industries**

Each sheet serves a distinct purpose.


## AML Knowledge Sheet

This is the core knowledge library. Each row represents an AML indicator mapped to a feature used in the final model.

### Columns

- **indicator_id**  
  Unique identifier assigned to each AML indicator.

- **segment**  
  Indicates whether the indicator applies to:
  - Business  
  - Personal  
  - Personal & Business  

- **supporting_information**  
  A concise description of the suspicious behavior, pattern, or risk rationale.  
  This field summarizes regulatory guidance or typology-based reasoning.

- **typology**  
  The money laundering typology associated with the indicator (e.g., Structuring, Layering, Placement, Shell Company).

- **feature**  
  The exact feature name used in the trained model.  
  All features listed are implemented features; no theoretical or unused features are included.

- **feature_logic**  
  A plain-language description of what the feature measures and how it captures the behavior described in the indicator.

- **citation**  
  The authoritative source supporting the indicator or typology (e.g., FINTRAC, FATF, academic literature).


## Methodology

### Indicator Identification
Indicators were identified using established AML guidance and typology literature. Each indicator reflects a behavioral pattern, transactional characteristic, or contextual signal commonly associated with ML risk.

### Typology Classification
Each indicator is categorized under a recognized AML typology to support structured interpretation and consistency.

### Feature Mapping
Each indicator is mapped directly to a feature used in the final model.  
Only indicators supported by implemented features were retained.

### Traceability
Each entry includes a citation to ensure traceability and defensibility.


## High Risk Industries Sheet

The **High Risk Industries** sheet provides a reference list of industries commonly associated with elevated money laundering risk.

Purpose of this sheet:
- Provide contextual awareness for business accounts  
- Support qualitative risk assessment  
- Complement indicator-level analysis  

This sheet is informational and does not introduce additional model features or scoring logic.


## How the Library Can Be Used

### For Modelling Experts
- Understand how AML indicators are operationalized through features  
- Support model explainability and documentation  
- Validate alignment between guidance and implementation  

### For Investigators
- Interpret why specific behaviors are flagged  
- Link model features to recognized AML typologies  
- Support investigative reasoning and reporting  

### For Compliance and Review
- Demonstrate structured use of AML guidance  
- Support transparency and auditability  
- Provide clear documentation of indicator rationale  


## Design Decisions

- Excel format selected for accessibility and ease of querying  
- Feature names strictly match implemented model features  
- Citations included directly in the library  
- Typology-based structure used for clarity  
- No speculative indicators or unused features included  


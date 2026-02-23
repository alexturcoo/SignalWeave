# 🧵 SignalWeave  
### A Weakly Supervised, Interpretable AML Risk Scoring Framework

> Weaving regulatory intelligence and behavioral signals into a scalable, transparent fraud detection system.

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

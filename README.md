# Network Intrusion Detection System (NIDS): Cost-Sensitive Ensemble Modelling

## Executive Summary
Modern network architectures require robust Intrusion Detection Systems (IDS) to identify malicious traffic in real-time. Traditional rule-based systems often struggle to catch novel, zero-day attacks. This project implements a machine learning-based behavioural approach, learning the mathematical signatures of normal versus anomalous network traffic based on the benchmark NSL-KDD dataset.

**Commercial Objective:** In a Security Operations Centre (SOC), the cost of a **False Negative** (missing an active cyberattack) is catastrophic compared to a **False Positive** (a false alarm). Therefore, this pipeline heavily prioritises recall and cost-sensitive learning to minimise missed attacks, culminating in advanced model interpretability to explain the algorithm's decisions to security analysts.

## Technical Stack
* **Language:** Python
* **Machine Learning:** Scikit-Learn (Random Forest Classifier)
* **Class Imbalance Handling:** Imbalanced-Learn (SMOTE)
* **Model Interpretability:** SHAP (SHapley Additive exPlanations)
* **Data Processing & Visualisation:** Pandas, NumPy, Matplotlib, Seaborn

## Core Methodology

### 1. Fault-Tolerant Data Simulation
To ensure 100% reproducibility without relying on external file hosting, the pipeline dynamically generates a high-fidelity synthetic dataset mimicking the continuous network flow metrics (e.g., `src_bytes`, `duration`) and categorical protocol types of the NSL-KDD dataset. It deliberately injects a realistic class imbalance, with intrusions representing a minority of total traffic.

### 2. Handling Class Imbalance (SMOTE)
Because normal traffic vastly outnumbers malicious traffic, a standard algorithm would become heavily biased. This pipeline applies the **Synthetic Minority Over-sampling Technique (SMOTE)** to the training data, generating synthetic attack signatures to perfectly balance the classes prior to modelling.

### 3. Cost-Sensitive Evaluation
The Random Forest ensemble is evaluated not just on accuracy, but on its ability to support SOC analysts:
* **Maximising Recall:** The model is evaluated heavily on Class 1 Recall to ensure malicious intrusions do not bypass the firewall undetected.
* **ROC-AUC & Confusion Matrices:** Visualisations are deployed to clearly illustrate the tradeoff between alert fatigue (False Positives) and security breaches (False Negatives).

### 4. Algorithmic Transparency (SHAP)
A 'black-box' model is useless in cybersecurity. When the NIDS flags a connection, analysts must know *why*. The pipeline utilises game-theoretic **SHAP values** via a `TreeExplainer` to generate a summary plot. This provides immediate, visual transparency into exactly which network protocols and flags (e.g., high `wrong_fragment` counts) mathematically drove the intrusion alert.

## How to Run
This notebook is entirely self-contained. 
1. Clone the repository.
2. Open `network_intrusion_detection.ipynb` in Jupyter Notebook or Google Colab.
3. Hit "Run All". The script will automatically install missing dependencies (like `shap` and `imbalanced-learn`), generate the data, train the model, and output the interpretability charts.

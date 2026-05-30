# 🏥 Frailty Risk Prediction & Explainable AI (XAI) Audit 

## 📌 Project Overview
This repository contains the research findings and documentation for a machine learning framework designed to stratify multidimensional frailty risk (Healthy, At-risk, Frail) using integrated health and social determinants. 

While modern ensemble models can achieve state-of-the-art predictive accuracy in healthcare, they often function as opaque "black boxes." This project investigates the critical trade-off between **algorithmic accuracy** and **clinical transparency**. By applying an Explainable AI (XAI) layer via SHAP, this study audits a highly accurate XGBoost model to expose hidden algorithmic biases (referred to as "Dark Logic"). Identifying these biases is crucial to ensure that Clinical Decision Support (CDS) systems do not automate or scale systemic healthcare inequalities.

## 🚀 Key Findings
1. **The Performance-Transparency Trade-off:** A baseline Logistic Regression model offered high transparency but resulted in a dangerous 16% False Negative rate for frail patients. 
2. **The Algorithmic Champion:** An XGBoost classifier significantly outperformed all other models, achieving **98.80% overall accuracy**, a **0.9996 ROC-AUC**, and catching 98% of vulnerable patients.
3. **The "Dark Logic" XAI Audit:** A subsequent SHAP audit revealed a severe systemic vulnerability. While the model correctly anchored its predictions in physiological metrics (identifying *Memory Score* as the top predictor), it heavily relied on socioeconomic proxies. The algorithm mathematically penalized patients with fewer years of education and lower income, artificially inflating their frailty risk score regardless of actual physical health.

## 📊 Dataset Description
The model is trained on a synthetic clinical dataset of 7,488 patient records encompassing 14 distinct multidimensional variables. 
* **Target Variable:** `aging_outcome` (Perfectly balanced: ~2,500 records each for Healthy, At-risk, and Frail).
* **Clinical Markers:** BMI, Blood Pressure, Chronic Conditions, Memory Score.
* **Lifestyle Factors:** Diet Quality, Physical Activity, Smoking Status, Alcohol Consumption.
* **Social Determinants:** Education Years, Income Level, Social Engagement.

## 🛠️ Methodology & Architecture
1. **Data Preprocessing:** Handled missing clinical behavioral data (alcohol consumption) via explicit "Unknown" imputation to preserve latent signaling rather than forcing artificial means. Applied Standard Scaling and One-Hot Encoding.
2. **Model Training:** Evaluated models across the interpretability spectrum:
   - *White-Box:* Logistic Regression (SAGA solver)
   - *Black-Box:* Random Forest, XGBoost, Neural Network (MLP)
3. **Validation:** 5-Fold Stratified Cross-Validation to ensure mathematical stability (Mean XGBoost Accuracy: 98.42% ±0.0021).
4. **Explainable AI (XAI):** Implemented TreeExplainer SHAP to calculate the marginal contribution of every feature, enabling both global feature importance ranking and local directional impact analysis (Beeswarm plots).

## 📂 Repository Structure
```text
├── data/                   # Dataset (CSV)
├── visuals/                # Exported SHAP plots (Global Importance, Beeswarm, etc.)
├── frailty_ml_paper.pdf    # Final IEEE formatted research paper 
└── README.md               # Project documentation

```

## 💻 Accessing the Code Pipeline

The complete, fully reproducible code pipeline for data processing, model training, and the SHAP audit is hosted on Kaggle.

🔗 **[View the Kaggle Notebook Here]**((https://www.kaggle.com/code/arpanakumari0924/explainable-frailty-prediction))

## 📝 Conclusion & Clinical Implications

High-performance black-box algorithms are necessary to accurately predict multidimensional frailty, as linear models miss too many vulnerable patients. However, this project proves that predictive accuracy cannot be the sole metric for clinical deployment. Unaudited models will default to socioeconomic proxies. To safely operationalize machine learning in Clinical Decision Support (CDS) systems, predictive models must be integrated into Human-in-the-Loop dashboards, ensuring clinicians can override mathematically biased recommendations.

---

**Author:** Arpana Kumari

**Academic Focus:** Machine Learning, Explainable AI (XAI), Healthcare Predictive Analytics

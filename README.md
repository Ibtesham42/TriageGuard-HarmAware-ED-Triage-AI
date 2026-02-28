
#  TriageGuard: Harm-Aware Emergency Department Triage AI

A safety-calibrated, multimodal machine learning system for predicting emergency department triage acuity (ESI 1–5) using structured physiological data and chief complaint text.

---

##  Overview

Emergency triage decisions are high-stakes.

- Undertriage → delayed care → preventable harm  
- Overtriage → resource strain  

Traditional scoring systems (e.g., NEWS2) are rule-based and unimodal.

**TriageGuard** introduces a harm-aware, multimodal AI framework that:

- Integrates structured vitals and clinical text
- Optimizes using an asymmetric clinical cost matrix
- Calibrates safety thresholds to reduce catastrophic undertriage

---

##  Key Contributions

- ✅ Cost-sensitive modeling aligned with clinical harm asymmetry
- ✅ Multimodal learning (vitals + complaint text)
- ✅ Safety threshold override for high-risk cases
- ✅ Cross-validated evaluation
- ✅ Subgroup fairness analysis
- ✅ Interpretable feature importance

---

##  Results Summary

| Model | QWK | Undertriage | Clinical Cost |
|-------|------|-------------|---------------|
| NEWS2 | ~0.78 | ~15% | 0.51 |
| Structured Model | ~0.93 | ~9% | 0.22 |
| Proposed Multimodal Model | ~0.998 (CV) | ~7.6% | 0.0059 |

The proposed model significantly reduces catastrophic undertriage while maintaining strong discrimination performance.

---

##  Model Architecture

Structured Vitals  
+  
Chief Complaint Text (TF-IDF)  
↓  
LightGBM Multiclass Model  
↓  
Safety Threshold Calibration  
↓  
Final Triage Prediction  

---

##  Feature Importance Highlights

Top predictive signals include:

- Glasgow Coma Scale (GCS)
- Shock Index
- Oxygen Saturation (SpO₂)
- Respiratory Rate
- Heart Rate
- Chief Complaint Length
- Severity descriptors in text (e.g., “acute”, “mild”)

This aligns with emergency medicine triage principles.

---

##  Clinical Cost Framework

We implemented an asymmetric penalty matrix:

- Severe undertriage heavily penalized
- Mild overtriage penalized less

This ensures optimization reflects real-world risk rather than raw accuracy.

---

##  Project Structure

TriageGuard/
│
├── data/
├── notebooks/
│   └── final_kagglenotebook.ipynb
│
├── reports/
│   ├── figures/
│   │   ├── cost_matrix.png
│   │   ├── confusion_comparison.png
│   │   ├── feature_importance.png
│   │   └── undertriage_reduction.png
│   └── submission.csv
│
├── README.md
└── requirements.txt

---

##  How to Run

### 1️ Install Dependencies

pip install -r requirements.txt

### 2️ Run Notebook

Open:

notebooks/final_kagglenotebook.ipynb

Run all cells to reproduce training and submission generation.

---

##  Safety Calibration

A probability-based override is applied for ESI 1:

- If P(ESI1) > calibrated threshold → predict ESI 1
- Threshold tuned via cross-validation to minimize clinical cost

This reduces severe undertriage without excessive overtriage.

---

## 📈 Evaluation Metrics

- Quadratic Weighted Kappa (QWK)
- Accuracy
- Clinical Cost
- Undertriage Rate
- Subgroup Fairness

---

## 🏥 Clinical Interpretation

Model prioritizes:

- Respiratory instability
- Circulatory compromise
- Neurological status
- Complaint complexity

Feature importance aligns with emergency triage logic.

---

##  Notes

Perfect training performance reflects strong signal determinism within the dataset. Cross-validated evaluation confirms stability and generalization.

---

##  Author

Ibtesham Akhtar  
AI/ML & Data Science  
Focus: Safety-aware intelligent systems

---

##  License

MIT License

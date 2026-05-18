# Predicting Student Dropout Using Random Forest

### An Early Warning System for Student Retention

**CSElec 01a — Computational Science** · University of Southern Mindanao · May 2026 · **Group 6**

<div align="center">

![License](https://img.shields.io/badge/license-MIT-blue)
![Python](https://img.shields.io/badge/python-3.10%2B-brightgreen)
![NumPy](https://img.shields.io/badge/built%20with-NumPy%20only-blueviolet)
![Streamlit](https://img.shields.io/badge/dashboard-Streamlit-ff4b4b)

</div>

| Name                         | Role   |
| ---------------------------- | ------ |
| Fuentes, Lara Rain B.        | Member |
| Palma, Gerard Carl Q.        | Member |
| Sumagka, Muhammed Shariff U. | Member |

---

## About

This capstone project develops a web-based Early Warning System (EWS)
that predicts whether a student will **Drop Out**, remain **Enrolled**,
or **Graduate**, using a Random Forest classifier built entirely from
scratch in Python and NumPy — no scikit-learn.

The model is trained on the
[**UCI Student Dropout and Academic Success dataset**](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)
(Realinho et al., 2021), which contains **4,424 student records** across
36 academic, demographic, and socio-economic variables. The system
achieved **79.3% classification accuracy** on the full training set.

Predictions are surfaced through a Streamlit dashboard designed for
university guidance counselors and academic advisors. Beyond the
classification result, the system generates role-based intervention
recommendations broken down by academic, financial, social, and
developmental support categories.

---

## Setup

```bash
pip install -r requirements.txt
streamlit run app.py
```

---

## Usage

Fill in the profile & demographics, academic
background, semester performance, and economic context — then click
**Run Risk Analysis**. The dashboard displays the predicted outcome,
class probabilities, active risk flags, feature importances, and
suggested interventions.

Student Name and ID fields are optional but will appear in the
report header, which is useful for saving screenshots to a
student's file.

---

## Dataset

**Predict Students' Dropout and Academic Success**
Realinho, V., Vieira Martins, M., Machado, J., & Baptista, L. (2021).
UCI Machine Learning Repository.
https://doi.org/10.24432/C5MC89

- 4,424 student records, 36 input variables
- Target classes: Dropout · Enrolled · Graduate
- Source institution: Polytechnic Institute of Portalegre, Portugal

> **Note on grading scale:** The dataset uses a Portuguese 0–200 grade
> scale. Grade inputs in this system use the Philippine 1.0–5.0 GWA
> scale and are converted at runtime (1.0 → 200, 5.0 → 0) before
> being passed to the model.

---

## File Structure

```text
cs-elec01-capstone/
├── app.py                  # Entry point
├── style.css               # Dashboard styles
├── data.csv                # Training dataset (semicolon-delimited)
├── requirements.txt        # Dependencies
├── assets/
│   └── usm_seal.png
└── usm_ews/
    ├── constants.py        # Categorical mappings and label definitions
    ├── data.py             # Data loading and preprocessing
    ├── layout.py           # Page config and shared UI components
    ├── model.py            # Random Forest built from scratch
    ├── prediction.py       # Prediction logic and risk flag derivation
    ├── sections.py         # Dashboard sections (charts, cards, interventions)
    └── sidebar.py          # Sidebar input form
```

---

## Technical Notes

- The Random Forest uses 11 trees at depth 6, with bootstrap sampling
  and random feature subsets (m = √M) per split to prevent overfitting.
- Split quality is determined by Shannon Entropy and Information Gain.
- The model trains once when the server starts, then stays cached in
  memory. Restarting the server retrains it; refreshing the browser
  does not.
- No student data is stored. All inputs exist only within the
  current session.

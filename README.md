# CW-FAS: Consensus-Weighted Feature-Augmented Stacking for Alzheimer's Classification

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: Negative Result](https://img.shields.io/badge/status-reproducible%20negative%20result-red.svg)](#)

A reproducible internal benchmark of **Consensus-Weighted Feature-Augmented Stacking (CW-FAS)** against nine baseline models on the synthetic **Rabie El Kharoua Alzheimer's Disease Dataset**.

**Central finding:** Consensus-augmented stacking does **not** improve Alzheimer's classification over well-tuned single tree ensembles on this synthetic tabular dataset. We report this as a **reproducible negative result**.

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Ablation Study](#ablation-study)
- [Reproducibility](#reproducibility)
- [Citation](#citation)
- [License](#license)

---

## Overview

The proposed pipeline (**CW-FAS**) combines:
1. **Mutual information** feature selection (K = 10)
2. **Six deterministic engineered features** (within-record composites)
3. **Four diverse base learners** — Random Forest (all features), XGBoost (MI-10), LightGBM (MI-10), Logistic Regression (standardized MI-10)
4. **A 3-dimensional consensus meta-feature block** — std across base learners, max pairwise disagreement, consensus entropy
5. **A regularized Logistic Regression meta-learner** (C = 0.5, class_weight='balanced')
6. **Isotonic calibration** on a held-out 20% slice

All metrics are computed from a **single frozen prediction file** (`predictions_v3.parquet`) to guarantee internal consistency.

---

## Dataset

- **Name:** Rabie El Kharoua Alzheimer's Disease Dataset
- **Source:** [Kaggle](https://www.kaggle.com/datasets/rabieelkharoua/alzheimers-disease-dataset)
- **N:** 2,149 records
- **Features:** 35 (41 after engineering)
- **Target:** Binary `Diagnosis` (0 = non-AD, 1 = AD)
- **Class distribution:** ~65% / ~35%
- **⚠️ Important:** This dataset is **synthetically generated**. The Kaggle page explicitly warns that it "may not reflect real-world data." No clinical claims are supported.

**Automatic download:** The notebook downloads the dataset via `kagglehub.dataset_download()` — no API token required.

---

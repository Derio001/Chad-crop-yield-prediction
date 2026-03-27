# 🌾 Chad Crop Yield Early Warning System

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![Data](https://img.shields.io/badge/Data-FAO%20%7C%20NASA%20POWER-green)](https://www.fao.org/faostat)
[![Models](https://img.shields.io/badge/Models-7%20Classifiers-orange)](https://scikit-learn.org/)
[![Best](https://img.shields.io/badge/Best%20Accuracy-XGBoost%2072.1%25-success)]()
[![Status](https://img.shields.io/badge/Status-Complete-brightgreen)]()

> **Can we predict a bad harvest year in Chad before it happens?**
> This project builds a machine learning early warning system for
> millet and sorghum — Chad's two staple crops — using 43 years
> of FAO yield data and NASA climate observations.

---

## 🌍 Why This Matters

Chad has one of the highest food insecurity rates in the world.
In 2024, over **6 million Chadians** faced acute food insecurity.
Yet most humanitarian responses are **reactive** — food aid
arrives months after a harvest has already failed.

**This project asks: can we predict bad harvest years in advance
using climate data — giving WFP, FAO, and the government of Chad
time to act before the crisis hits?**

---

## 📊 Data Sources

| Source | Data | Coverage |
|--------|------|----------|
| [FAO FAOSTAT](https://www.fao.org/faostat) | Millet & Sorghum yield, area, production | Chad 1961–2024 |
| [NASA POWER MERRA-2](https://power.larc.nasa.gov/) | Rainfall, Temp Mean/Max/Min | Chad 1981–2025 |

**Modeling period:** 1982–2024 (43 years after lag feature creation)

---

## 🔬 Methodology
```
FAO Crop Data + NASA Climate Data
        ↓
Data Cleaning & Merging (43 years overlap)
        ↓
EDA — Yield trends, rainfall patterns, correlation analysis
        ↓
Feature Engineering
(Lag features, rainfall anomaly, temperature range,
rainfall category)
        ↓
Regression Models → Poor performance → Problem reframed
        ↓
Binary Classification
(Bad year = below median yield)
        ↓
7 Classifiers benchmarked (LOO Cross-Validation)
        ↓
Early Warning System
```

---

## 🚨 Key Findings

### 1. Rainfall alone cannot predict crop failure
Bad harvest years had almost identical rainfall to good years
(548mm vs 557mm average). **Rainfall is not the primary driver
of crop failure in Chad.**

### 2. Drought is the default condition
**65% of years between 1981–2024 had below-average rainfall.**
Chad's farmers operate under chronic water stress, not
occasional drought.

### 3. Cascading failures are real
Last year's yield is the strongest predictor of this year's
yield for both crops. A bad year tends to be followed by
another bad year — compounding food crises.

### 4. Millet vs Sorghum respond differently
- **Millet** is more sensitive to temperature anomalies
- **Sorghum** responds more to rainfall category
- Sorghum is more predictable and more drought-resilient

---

## 🤖 Model Results

### Classification — Bad Year Prediction

| Model | Millet Accuracy | Sorghum Accuracy |
|-------|----------------|-----------------|
| **Logistic Regression** | **62.8% ✅** | 60.5% |
| CART Decision Tree | 60.5% | 72.1% |
| Random Forest | 58.1% | 67.4% |
| **XGBoost** | 60.5% | **72.1% ✅** |
| Gradient Boosting | 55.8% | 65.1% |
| CatBoost | 53.5% | 67.4% |
| KNN | 58.1% | 60.5% |
| Baseline (random) | 50.0% | 50.0% |

All models evaluated using **Leave-One-Out Cross Validation**
— the most rigorous approach for small datasets (43 samples).

### Early Warning Thresholds
- 🌾 Millet bad year: yield **< 517 kg/ha**
- 🌾 Sorghum bad year: yield **< 703 kg/ha**

---

## 🔑 Most Important Features

**Millet (Logistic Regression):**
1. Last year's sorghum yield — cascading failure signal
2. Mean temperature — heat stress indicator
3. Rainfall anomaly — deviation from long-term average

**Sorghum (XGBoost):**
1. Rainfall category — drought vs normal vs good
2. Maximum temperature — peak heat stress
3. Last year's sorghum yield — momentum effect

---

## 📁 Project Structure
```
chad-crop-yield-prediction/
│
├── Chad_Crop_Yield_Prediction.ipynb   # Full analysis (32 cells)
├── chad_crop_climate_merged.csv       # Final merged dataset
├── model_comparison_results.csv       # All model results
│
├── data/
│   ├── Agri_chad.csv                  # FAO crop production data
│   ├── Nasa_Climate_data_chad.csv     # NASA POWER climate data
│   └── README.md                      # Data download instructions
│
└── README.md
```

---

## 🚀 How to Run
```bash
# Clone
git clone https://github.com/Derio001/chad-crop-yield-prediction
cd chad-crop-yield-prediction

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn 
pip install xgboost catboost

# Run notebook
jupyter notebook Chad_Crop_Yield_Prediction.ipynb
```

---

## 🔭 Future Work

- [ ] Add conflict/fragility index as a feature
- [ ] Incorporate regional disaggregation (Sahel vs South Chad)
- [ ] Add more crops (groundnut, sesame, maize)
- [ ] Build a Streamlit early warning dashboard
- [ ] Integrate FEWS NET food security phase data
- [ ] Extend to neighboring Sahel countries (Niger, Mali, Sudan)

---

## 📌 Policy Implications

This model has direct applications for:
- **WFP Chad** — pre-position food aid before harvest failure
- **FAO Chad** — target agricultural interventions by region
- **Government of Chad** — budget planning for food imports
- **UNICEF Chad** — anticipate child malnutrition spikes

---

## 👤 Author

**Mahamat Hanga Derio**
M.Tech Data Science — Christ University, Bangalore
Chadian national | Building data-driven solutions for
food security and development in Sub-Saharan Africa

📬 Open to collaboration with WFP, FAO, NGOs and research
institutions working on food security in the Sahel
🔗 [GitHub](https://github.com/Derio001) |
[LRI Health Project](https://github.com/Derio001/lri-prediction-chad) |
[GDP Dashboard](https://github.com/Derio001/exploratory-predictive-gdp-analysis)

---

*Part of a portfolio of data science projects focused on
public health and economic development in Chad and the
Lake Chad Basin.*

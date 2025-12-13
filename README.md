# Exploring Machine Learning Approaches for Temperature Variability Using GHCNd Data

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)
[![NOAA GHCN-D](https://img.shields.io/badge/Data-NOAA%20GHCN--D-orange.svg)](https://doi.org/10.7289/V5D21VHZ)
[![Made with Dask](https://img.shields.io/badge/Parallelized%20with-Dask-FF6F00.svg)](https://www.dask.org)
[![Scikit-Learn](https://img.shields.io/badge/ML-ScikitLearn-4D9ACF.svg)](https://scikit-learn.org/)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626.svg)](https://jupyter.org)

This project applies supervised and unsupervised machine learning techniques to analyze daily maximum temperature (TMAX) observations from the NOAA Global Historical Climatology Network – Daily (GHCN-D).  
The goal is to assess the predictability of daily temperature anomalies and identify climate-driven station clusters across the contiguous United States.

---

## 📌 Motivation

1. **Understanding Regional Climate Behavior**  
   Daily temperature variability reflects synoptic patterns, land–atmosphere interactions, and regional climate regimes. Clustering stations reveals meaningful physical groupings.

2. **Evaluating Machine Learning for Climate Research**  
   ML provides a flexible framework to predict temperature anomalies and classify above/below-normal days, complementing traditional statistical climate tools.

3. **Leveraging a Long-Term, High-Quality Dataset**  
   GHCN-D provides decades of spatially distributed daily temperature data, enabling robust ML evaluation across diverse climates.

---

## 📂 Data Source

**NOAA GHCN-Daily**  
- Accessed via NOAA CDO API  
- Each station file includes daily TMAX values  
- Anomalies computed relative to **1991–2020 climate normals**

🔗 DOI: https://doi.org/10.7289/V5D21VHZ

---

## 🔍 Methods

### **1. Data Preprocessing**
- Automatic retrieval of GHCN station metadata
- Download and cleaning of daily TMAX records
- Removal of missing or low-quality entries
- Computation of anomalies relative to 1991–2020 normals
- Parallelized processing using **Dask** for efficiency

### **2. Supervised Machine Learning**
Models applied per station:
- **Logistic Regression** – classify above/below-normal days  
- **Random Forest Classifier** – nonlinear classification  
- **Linear Regression & RF Regression** – predict anomaly magnitude  

Metrics:
- Accuracy, ROC-AUC (classification)  
- RMSE, R² (regression)

### **3. Unsupervised Learning (Clustering)**
- Monthly mean + monthly standard deviation of TMAX (24 features)
- Standardized and clustered using **K-Means (K=5)**
- Regional interpretations of cluster structure
- Visualizations:
  - Mean monthly TMAX cycle per cluster
  - Cluster–region heatmap
  - Station spatial distribution

---

## 📈 Key Results Summary

### **Classification**
- Accuracy: **0.72–0.74**
- ROC-AUC: **0.79–0.83**
- RF > Logistic Regression (captures nonlinear behavior)

### **Regression**
- RMSE: **0.52–0.57°C**
- R²: **0.91–0.92**

These values are physically consistent given natural synoptic-scale temperature variability.

### **Clustering**
- Stations grouped into coherent climate regimes  
- Clusters reflect seasonal cycle amplitude and variability  
- Replacement stations integrate seamlessly into clusters  
- Some regions show tighter grouping (e.g., Southeast), while others are more diverse (e.g., Southwest/Northwest transition zones)

---

## 📁 Repository Structure

project/
│
├── data/
│ ├── raw/ # Raw downloaded GHCN-D files
│ ├── processed/ # Cleaned processed station data
│
├── notebooks/
│ ├── analysis.ipynb # Main analysis workflow
│ ├── clustering.ipynb # Station clustering workflow
│
├── station_clusters_kmeans.csv
├── README.md
└── LICENSE

---

## 📦 Requirements

Key packages used:
numpy
pandas
datetime
matplotlib
scikit-learn
dask
requests
tqdm
xarray
seaborn

---

## 📜 MIT License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
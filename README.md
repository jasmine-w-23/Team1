About
(UNSW-NB15)
. https://www.kaggle.com/datasets/alextamboli/unsw-nb15/data

(CIC-IDS2017)
. https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset/data

We merged the 1-4 CSV files into one raw file and applied the cleaning and feature functions. 
Additionally, after generating the statistical scales, we reduced the cleaned CSV file to 25% to limit the size to under 70MB. 
The smaller one is for model training.


CIC-IDS2017 — Cleaning + Feature
------------------------------------------------------------------------
What this script does:
1) Load all CIC-IDS2017 CSVs from INPUT_DIR (glob patterns provided)
2) Clean:
   - normalize column names
   - replace 'Infinity', 'inf', 'NaN' strings -> NaN, then fill numerics with 0, strings with ""
   - drop duplicates
   - map labels: Benign -> 0, anything else -> 1
   - normalize timestamps ('Timestamp' variants) to epoch/hour/weekday
3) Feature creation:
   - ratios: fwd/bwd packets & bytes (if columns present)
4) Encoding:
   - one-hot only a few categoricals (Protocol, Service, State), capped to Top-K to avoid explosion
5) Scaling:
   - Standard or MinMax on numeric columns (NumPy only)
6) Feature selection:
   - drop highly correlated (> 0.98 abs) columns
7) Dimensionality reduction:
   - PCA via NumPy (keep 95% variance)
8) Save:
   - cleaned CSV.GZ, summary_stats.csv, correlation_heatmap.png, pca_scatter.png

Dependencies: pandas, numpy, matplotlib
"""

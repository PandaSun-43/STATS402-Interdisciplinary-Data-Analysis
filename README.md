# STATS402-Interdisciplinary-Data-Analysis
Comparison of Spatio-Temporal Models (GPR/GAM) vs Traditional ML (LR/RF/SVR) for Nitrogen Fixation Prediction

## Project Description
This project compares traditional machine learning (Random Forest, SVR) with spatio-temporal models (Gaussian Process Regression, Generalized Additive Models) to predict global oceanic N₂ fixation rates. It improves upon Tang et al. (2019) by:
- Incorporating iron (Fe) as a new predictor
- Explicitly modeling spatio-temporal interactions
- Providing uncertainty quantification

## Setup Instructions
### Dependencies
- Python 3.8+
- Required packages: numpy, pandas, scipy, matplotlib, seaborn, scikit-learn, pygam, cartopy
- Install via: ```bash
pip install -r requirements.txt

## Data Preparation
1. Place raw data files in /data/raw/ (SST, PAR, CHL, etc.)
2. Run notebooks in order:
   1_data.ipynb → 2_EDA.ipynb → 5_CreateVarFile.ipny → [3_GPR|4_GAM|6_MLModel].ipynb

## How to Run
1. For data matching and analysis: Run 1_data.ipynb and 2_EDA.ipynb
2. For model training/prediction:

GPR: Run 3_GPR.ipynb

GAM: Run 4_GAM.ipynb

Traditional ML: Run 6_MLModel.ipynb

3. For visualizations:
   
Global maps are generated automatically in each notebook.

Use 7_Figures.ipynb to combine plots.

## Known Limitations
1. Temporal resolution: Monthly averages may miss short blooms.
2. Computational demand: GPR cost a lot in computation for global predictions.
3. Data gaps: Points sparse in Southern Ocean.




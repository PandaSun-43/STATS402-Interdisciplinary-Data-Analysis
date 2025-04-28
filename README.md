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

## Overview of the code files
1. 1_data.ipynb: The data for SST, PAR, Chl, Salinity, DO, N, P are downloaded from websites and decompressed.The data for iron(Fe) is newly added here as a variable. Match all of these variables to the N2 fixation dataset. Based on month, divide the dataset into 80% training set and 20% test set.
2. 2_ExploratoryDataAnalysis.ipynb: Analyze the dataset through the distribution of N2 fixation points, the distribution (boxplot and histogram) of all the environmental variables, and correlation matrix.
3. 3_GPR.ipynb: Implementation and optimization (GridSearchCV) of GPR model, with some visualizations showing the kernel function of the model. Use the best estimator to do the prediction and plot the scatter plot (observed vs predicted value) + the uncertainty quantification. Use visualizations to analyze the importance of each variable in different regions (global vs tropics vs temperate). Then, generate monthly global prediction + uncertainty, and annual average global prediction + uncertainty.
4. 4_GAM.ipynb: Implementation of GAM model. Analyze the residuals of different variable pairs. Based on the environmental knowledge and residual analysis, add interaction terms into the GAM model. Then, do the prediction and plot the scatter plot (observed vs predicted value). Visualize the PDPs of each variable to find the threshold and turning point. For the added interaction pairs, visualize the heatmap to show their synergistic effect on N2 fixation. Finally, generate monthly global prediction + annual average global prediction.
5. 5_CreateVarFile.ipynb: A file to handle the .mat data files (SST, PAR, CHL). Since these variables are collected every 8 days. But for the global prediction, I need to generate a monthly prediction. So, I generated the files of SST/PAR/CHL for each month through calculating the mean values of all the .mat files within each month. (For example, January files: ['sst.2023017.hdf.mat', 'sst.2023025.hdf.mat', 'sst.2023009.hdf.mat', 'sst.2023001.hdf.mat']. February files: ['sst.2023049.hdf.mat', 'sst.2023033.hdf.mat', 'sst.2023041.hdf.mat', 'sst.2023057.hdf.mat']).
6. 6_MLModel.ipynb: Implementation and optimization (GridSearchCV) of LR/RF/SVR. Use the best estimator to do the 3 predictions and plot the scatter plots (observed vs predicted value). In this code file, I did some preparations for the global map plot: resampled all the variables monthly into a (180,360) grid and stored them in .npz files, which makes the plotting more convenient. Finally, generate monthly global prediction + annual average global prediction for LR/RF/SVR.
7. 7_Figures.ipynb: Simply used to merge 5 global plots into 1 figure.

## Known Limitations
1. Temporal resolution: Monthly averages may miss short blooms.
2. Computational demand: GPR cost a lot in computation for global predictions.
3. Data gaps: Points sparse in Southern Ocean.




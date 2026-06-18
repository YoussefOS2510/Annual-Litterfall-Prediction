# Project README: Annual Litterfall Prediction

## Overview
This project aims to analyze and predict the **Total Annual Litterfall (Mg per ha per yr)** based on various environmental and forest characteristics using R. The analysis spans data cleaning, exploratory data analysis (EDA), and the implementation of multiple regression models.

## Data Description
The dataset includes several key variables:
- **Geographic**: Latitude, Longitude, Altitude(m).
- **Climatic**: MAT (Mean Annual Temperature), MAP (Mean Annual Precipitation).
- **Forest Characteristics**: Forest type, Stand origin, Age, DBH, Height, and Density.
- **Litterfall Components**: Leaf, Branch, Reproduction, and others.

## Workflow

### 1. Data Preprocessing
- **Library Loading**: Utilizes `readxl`, `randomForest`, `e1071`, `rpart`, and `ggplot2`.
- **Cleaning**: 
  - Handled missing values by imputing column means.
  - Categorical variables (`Forest type`, `Stand origin`) were encoded into numeric integers.
  - Outliers were identified using the Interquartile Range (IQR) method.
  - Feature selection: Removed specific redundant or high-null columns (e.g., indices 8, 9, 16).

### 2. Exploratory Data Analysis (EDA)
- Generated histograms for numeric distributions.
- Created scatter plots to visualize relationships between environmental factors and Total Litterfall.
- Conducted a **Correlation Analysis**, finding that `Leaf` and `Branch` mass have the strongest positive correlation with Total Litterfall, while `Latitude` shows a significant negative correlation.

### 3. Model Development & Evaluation
The data was split into an 80% Training set and a 20% Test set. The following models were evaluated using MSE, RMSE, MAE, and R-squared:

| Model | R-squared (Approx) | Notes |
| :--- | :--- | :--- |
| **Linear Regression** | 0.849 | Good baseline performance. |
| **SVM (Radial Kernel)** | 0.828 | Stable, but slightly higher error than Linear Regression. |
| **Decision Tree** | 0.768 | Pruned using CP=0.01; provides high interpretability. |
| **Random Forest** | **0.894** | **Best Performer**; handled non-linearities effectively. |
| **Polynomial Regression**| 0.857 | Improved slightly over standard Linear Regression. |

## Conclusion
The **Random Forest** model provided the most accurate predictions for annual litterfall in this dataset. Biological components like Leaf and Branch mass remain the most critical predictors, followed by climatic variables like MAT.
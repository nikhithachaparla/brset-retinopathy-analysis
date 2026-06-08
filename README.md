# Diabetic Retinopathy Risk Analysis — BRSET Dataset

## Overview
Exploratory data analysis and machine learning study using the Brazilian 
Multilabel Ophthalmological Dataset (BRSET) — 16,266 retinal fundus images 
from 8,524 Brazilian patients. This project investigates clinical and 
demographic predictors of diabetic retinopathy using structured patient data.

## Research Question
Can patient demographics and anatomical parameters predict diabetic 
retinopathy without relying on retinal image analysis?

## Dataset
- **Source:** BRSET — Brazilian Multilabel Ophthalmological Dataset (PhysioNet)
- **Size:** 16,266 images from 8,524 patients
- **Labels:** 13 multilabel ophthalmological conditions
- **Target variable:** Diabetic retinopathy (binary, 6.8% prevalence)

## Data Access
The BRSET dataset requires credentialed access through PhysioNet.

- **Access:** Register and complete required training at physionet.org
- **Dataset page:** https://physionet.org/content/brazilian-ophthalmological/
- **Raw data is NOT included in this repository** in compliance with 
  PhysioNet data use agreement
- To reproduce this analysis, download the dataset after obtaining 
  access and place `labels.csv` in the root directory

## Key Findings

### Clinical Insights
- Patients aged 50-80 had the highest absolute number of DR cases,
  consistent with Type 2 diabetes prevalence in this age group
- The 20-30 age group showed the highest DR rate (10.3%) — attributed 
  to longer Type 1 diabetes duration rather than age itself
- Male patients had nearly double the DR rate of females (9.5% vs 4.9%),
  consistent with literature on sex differences in diabetes management
- Macular edema was the most common condition co-occurring with DR,
  confirming the shared vascular pathology between the two conditions
- 88% of diabetes duration data was missing — a real-world data quality
  challenge handled through feature selection

### Model Performance
| Model | ROC-AUC | DR Recall | DR F1 |
|---|---|---|---|
| Logistic Regression | 0.830 | 0.813 | 0.314 |
| Random Forest | 0.735 | 0.463 | 0.263 |
| KNN | 0.691 | 0.097 | 0.157 |

- Logistic Regression performed best — ROC-AUC 0.830, catching 81.3% 
  of actual DR cases
- KNN achieved 92.9% accuracy but only 9.7% DR recall — demonstrating 
  that accuracy is a misleading metric for imbalanced clinical data
- Patient age and macula grading were the strongest predictors of DR

## Methods
- Data cleaning: filtered to adequate quality images (n=14,279)
- Handled missing data: excluded columns with >80% missingness
- Class imbalance: addressed using class_weight='balanced'
- Evaluation: prioritized recall over accuracy for clinical relevance
- Models: Logistic Regression, Random Forest, KNN with stratified 
  train/test split (80/20)

## Technologies
Python, pandas, scikit-learn, matplotlib, seaborn

## Project Structure

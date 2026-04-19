# Protein Structure Classification Using Machine Learning

This repository contains the source code, notebooks, and detailed project report for the **Protein Structure Classification** project. The objective of the project is to leverage machine learning techniques to classify proteins based on their structural and experimental attributes. This work demonstrates a robust data preprocessing pipeline, exploratory data analysis (EDA), and the development of effective classification models.

---

## Table of Contents

- [Protein Structure Classification Using Machine Learning](#protein-structure-classification-using-machine-learning)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Dataset Overview](#dataset-overview)
  - [Methodology](#methodology)
  - [Model Building](#model-building)
    - [K-Nearest Neighbors (KNN) Classifier](#k-nearest-neighbors-knn-classifier)
      - [Model Development](#model-development)
    - [Random Forest Classifier](#random-forest-classifier)
      - [Model Development](#model-development-1)
    - [Comparative Analysis and Performance Summary](#comparative-analysis-and-performance-summary)
      - [Summary Table of Performance Metrics](#summary-table-of-performance-metrics)
  - [Conclusion](#conclusion)
  - [Limitations and Future Work](#limitations-and-future-work)
  - [Usage](#usage)
  - [Authors](#authors)

---

## Overview

This project aims to develop predictive models for protein classification by using machine learning techniques. By analyzing structural attributes and experimental data, our approach extracts meaningful patterns that differentiate protein classes. The project showcases the practical application of algorithms like K-Nearest Neighbors (KNN) and Random Forest, along with advanced hyperparameter tuning using GridSearchCV.

---

## Dataset Overview

- **Source:**  
  The dataset is obtained from Kaggle and originally sourced from the RCSB Protein Data Bank (PDB).

  Dataset Link: [Structural Protein Sequences](https://www.kaggle.com/datasets/shahir/protein-data-set)

- **Contents:**  
  - Two CSV files: 
    - `pdb_data_no_dups.csv`: Contains protein metadata (e.g., classification, experimental technique).
    - `data_seq.csv`: Contains over 400,000 protein structure sequences.
  - After data cleaning, the dataset includes 111,332 records and 16 features.

- **Key Features:**  
  - **structureId:** Unique identifier for each protein.
  - **classification:** Target variable representing protein classes.
  - **experimentalTechnique, macromoleculeType, residueCount, resolution, structureMolecularWeight,** etc.

---

## Methodology

The project workflow includes:
1. **Data Preparation & Cleaning:**  
   Filtering the dataset to include only proteins (i.e., "Protein" and "Protein#RNA") obtained via X-ray diffraction, removing duplicates and null values, and encoding the target variable.
   
2. **Exploratory Data Analysis (EDA):**  
   Generating statistical summaries, correlation matrices, and visualizations (heatmaps, pair plots) to understand feature relationships.
   
3. **Model Building:**  
   Developing and tuning two models – KNN and Random Forest – to classify proteins into three target classes (Hydrolase, Transferase, Oxidoreductase).

---

## Model Building

### K-Nearest Neighbors (KNN) Classifier

#### Model Development

- **Objective:**  
  Classify proteins based on numerical features using the KNN algorithm.

- **Preprocessing:**  
  The feature set is standardized using `StandardScaler` to ensure equal contribution of all variables in the distance calculations.

- **Hyperparameter Tuning:**  
  The model was tested with different values of *k* using the Elbow Method. The best performance was achieved with **k = 1**.

---

### Random Forest Classifier

#### Model Development

- **Objective:**  
  Enhance predictive accuracy by aggregating the outputs of multiple decision trees.

- **Preprocessing:**  
  Features are scaled using `StandardScaler` to maintain consistency.

- **Hyperparameter Tuning with GridSearchCV:**  
  To identify the optimal hyperparameters, GridSearchCV was used to explore various combinations of `n_estimators`, `max_features`, and `bootstrap` settings. The following code snippet illustrates the tuning process:

  ```python
  from sklearn.model_selection import GridSearchCV

  param_grid = {
      'n_estimators': [21, 30, 40, 50],
      'max_features': [2, 3, 4, 5],
      'bootstrap': [True, False]
  }

  rf_cv = RandomForestClassifier(random_state=42)
  grid = GridSearchCV(rf_cv, param_grid, cv=3)
  grid.fit(X_train_scaled, y_train)

  print("Best parameters found:", grid.best_params_)

  rf_best = grid.best_estimator_
  rf_best_preds = rf_best.predict(X_test_scaled)
  print(classification_report(y_test, rf_best_preds))
  ```
---

### Comparative Analysis and Performance Summary

Both models showed promising results for protein classification. While the KNN model (with k = 1) provided a simple yet effective baseline, the Random Forest classifier demonstrated enhanced performance due to its ensemble nature and rigorous hyperparameter tuning.

#### Summary Table of Performance Metrics



| **Model**                  | **Accuracy** | **Hydrolase (Prec/Rec/F1)** | **Transferase (Prec/Rec/F1)** | **Oxidoreductase (Prec/Rec/F1)** |
|----------------------------|--------------|-----------------------------|-------------------------------|--------------------------------|
| **KNN (k = 1)**            | 0.86          | 0.87 / 0.86 / 0.86             | 0.83 / 0.84 / 0.84               | 0.87 / 0.87 / 0.87                |
| **Random Forest (Tuned)**  | 0.91          | 0.89 / 0.93 / 0.91             | 0.90 / 0.89 / 0.90               | 0.95 / 0.90 / 0.92                |



---

## Conclusion

The model-building process confirms that machine learning techniques can effectively classify protein structures into distinct functional categories. The KNN model provides a straightforward solution, while the Random Forest model—enhanced through GridSearchCV hyperparameter tuning—offers superior performance and robustness. These results illustrate the feasibility of applying advanced machine learning techniques to complex biological datasets.

---

## Limitations and Future Work

While the current study demonstrates promising results, several limitations and opportunities for future research remain:

1. **Limited Class Scope:**  
   The model currently predicts only three protein classes. Future work could expand the classification to include a wider variety of protein categories for a more comprehensive analysis.

2. **Dataset Scale:**  
   Testing the model on larger, more diverse datasets will help assess scalability and improve generalization across different protein types.

3. **Feature Multicollinearity:**  
   Addressing multicollinearity among features may enhance model stability and interpretability, leading to more robust predictions.

4. **Computational Efficiency:**  
   Optimizing the model architecture and exploring more efficient algorithms are necessary to manage computational costs as dataset size increases.

---

## Usage
- Open the provided Google Colab Notebook.
- Mount your Google Drive and update file paths as necessary.
- Run the notebook cells sequentially to execute data preprocessing, EDA, and model building.

---

## Authors

**Project By:**  Adinath Desai


---

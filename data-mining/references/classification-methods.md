# Classification Methods

Supervised learning techniques for categorizing data into predefined classes, covering algorithm selection, feature engineering, and model evaluation.

---

## Algorithm Selection Guide

| Algorithm | Best For | Interpretability | Scales To | Handles Missing Data |
|-----------|---------|-----------------|-----------|---------------------|
| Logistic Regression | Binary/multi-class, baseline model | High | Large datasets | No (impute first) |
| Decision Tree | Explainable rules, mixed data types | Very High | Medium datasets | Yes (some implementations) |
| Random Forest | General purpose, robust | Medium | Large datasets | Partially |
| Gradient Boosting (XGBoost/LightGBM) | Tabular data competitions, high accuracy | Low-Medium | Large datasets | Yes |
| SVM | High-dimensional, clear margins | Low | Medium datasets | No |
| k-Nearest Neighbors | Simple baseline, small datasets | Medium | Small datasets | No |
| Naive Bayes | Text classification, fast baseline | High | Large datasets | Yes |
| Neural Networks | Complex patterns, large data | Low | Very large datasets | No |

## Feature Engineering for Classification

### Categorical Encoding

| Technique | When to Use | Example |
|-----------|-------------|---------|
| One-Hot Encoding | Low cardinality (<15 categories) | Color: Red→[1,0,0], Blue→[0,1,0] |
| Label Encoding | Ordinal categories | Size: S→1, M→2, L→3 |
| Target Encoding | High cardinality, tree models | City → average target value per city |
| Frequency Encoding | When category frequency matters | City → proportion of records with that city |
| Binary Encoding | Medium-high cardinality | Category ID → binary representation |

### Feature Scaling

- **StandardScaler**: Zero mean, unit variance. Use for SVM, logistic regression, and neural networks.
- **MinMaxScaler**: Scale to [0, 1]. Use when features need bounded values.
- **RobustScaler**: Uses median and IQR. Preferred when outliers are present.
- Tree-based models (Random Forest, XGBoost) do not require feature scaling.

### Feature Selection Methods

1. **Filter methods**: Correlation analysis, chi-squared test, mutual information — fast but ignores feature interactions
2. **Wrapper methods**: Recursive Feature Elimination (RFE) — uses the model to rank features by importance
3. **Embedded methods**: L1 regularization (Lasso), tree-based feature importance — built into the training process

## Handling Imbalanced Classes

| Technique | Description | When to Use |
|-----------|-------------|-------------|
| SMOTE | Generate synthetic minority examples | Moderate imbalance (1:5 to 1:20) |
| Random Undersampling | Remove majority examples | Large dataset, mild imbalance |
| Class Weights | Penalize misclassifying minority class | First approach to try |
| Threshold Tuning | Adjust decision threshold from 0.5 | When precision-recall tradeoff matters |
| Ensemble (EasyEnsemble) | Train multiple models on balanced subsets | Severe imbalance |

## Model Evaluation

### Metrics Beyond Accuracy

| Metric | Formula | Use When |
|--------|---------|----------|
| Precision | TP / (TP + FP) | Cost of false positives is high (spam detection) |
| Recall | TP / (TP + FN) | Cost of false negatives is high (disease diagnosis) |
| F1 Score | 2 × (Precision × Recall) / (Precision + Recall) | Balance between precision and recall |
| AUC-ROC | Area under ROC curve | Overall ranking quality |
| Log Loss | −Σ[y·log(p) + (1−y)·log(1−p)] | Probability calibration matters |
| Cohen's Kappa | Agreement beyond chance | Multi-class, imbalanced data |

### Cross-Validation Strategies

- **Stratified K-Fold** (k=5 or 10): Preserves class proportions in each fold. Default choice.
- **Repeated Stratified K-Fold**: Run k-fold multiple times with different random splits for more stable estimates.
- **Time Series Split**: For temporal data, train on past and validate on future. Never shuffle.
- **Group K-Fold**: When data contains groups (e.g., patients) that should not span train and test sets.

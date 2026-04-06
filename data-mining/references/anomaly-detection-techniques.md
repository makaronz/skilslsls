# Anomaly Detection Techniques

Methods for identifying unusual patterns, outliers, and deviations in data that may indicate fraud, system failures, or novel insights.

---

## Anomaly Types

| Type | Description | Example |
|------|-------------|---------|
| Point Anomaly | A single data point deviates significantly from the rest | A $50,000 transaction in an account averaging $200 |
| Contextual Anomaly | A data point is anomalous in a specific context but normal otherwise | 30°C temperature is normal in summer, anomalous in winter |
| Collective Anomaly | A group of data points together form an anomalous pattern | A sequence of small transactions that individually look normal but collectively indicate structuring |

## Statistical Methods

### Z-Score Method

Calculate the number of standard deviations a point is from the mean:

```
Z = (x − μ) / σ
```

Flag points with |Z| > 3 as anomalies. Works well for normally distributed data. For skewed distributions, apply a log transform first or use the Modified Z-Score with the median absolute deviation (MAD):

```
Modified Z = 0.6745 × (x − median) / MAD
```

### IQR Method

Use the interquartile range to define boundaries:

```
Lower Fence = Q1 − 1.5 × IQR
Upper Fence = Q3 + 1.5 × IQR
```

Points outside the fences are flagged. More robust to non-normal distributions than Z-score. Adjust the multiplier (1.5 for outliers, 3.0 for extreme outliers).

### Grubbs' Test

A formal statistical test for a single outlier in a univariate dataset. Calculates a test statistic and compares it to a critical value based on the sample size and significance level. Apply iteratively to detect multiple outliers.

## Machine Learning Methods

### Isolation Forest

Isolation Forest isolates anomalies by randomly selecting features and split values. Anomalies are easier to isolate (fewer splits needed), so they have shorter average path lengths in the ensemble of random trees.

Key parameters:
- `n_estimators`: Number of trees (100-300 typical)
- `contamination`: Expected proportion of anomalies (0.01-0.1)
- `max_samples`: Subsample size per tree (256 is usually sufficient)

Advantages: Scales well to high-dimensional data, does not assume a distribution, handles mixed feature types.

### Local Outlier Factor (LOF)

LOF compares the local density of a point to the density of its neighbors. A point with substantially lower density than its neighbors is flagged as an outlier. The LOF score quantifies this:

- LOF ≈ 1: Similar density to neighbors (inlier)
- LOF >> 1: Much lower density than neighbors (outlier)

Key parameter: `n_neighbors` (20 is a common default). Sensitive to the choice of k, so try multiple values.

### Autoencoders

Train a neural network to compress and reconstruct normal data. The reconstruction error for normal data will be low, while anomalies produce high reconstruction error because the model has not learned to represent them.

Architecture: Input → Encoder (compress to bottleneck) → Decoder (reconstruct) → Output. Set the anomaly threshold at a percentile of reconstruction errors on the validation set (e.g., 95th or 99th percentile).

## Time Series Anomaly Detection

| Method | Use Case | Implementation |
|--------|----------|---------------|
| STL Decomposition + Residual Thresholding | Seasonal data with regular patterns | Decompose, threshold residuals at ±3σ |
| Prophet Anomaly Detection | Business metrics with holidays and trends | Use Prophet's uncertainty intervals |
| ARIMA Residuals | Stationary or differenced time series | Flag residuals exceeding confidence bounds |
| Streaming Detection (ADWIN) | Real-time data streams | Detect distribution changes in sliding windows |

## Evaluation Metrics

Anomaly detection is typically an imbalanced classification problem. Use:

- **Precision**: Of flagged anomalies, how many are true anomalies? (Reduces alert fatigue)
- **Recall**: Of all true anomalies, how many did we catch? (Reduces missed detections)
- **F1 Score**: Harmonic mean of precision and recall
- **AUC-PR**: Area under the Precision-Recall curve (preferred over AUC-ROC for imbalanced data)

# Data Quality Report

## Monday Dataset

- Rows: 529,918
- Columns: 79
- Memory Usage: 343.15 MB

---

## Missing Values

| Column | Missing Values |
|----------|---------------|
| Flow Bytes/s | 64 |

Percentage of missing values:

```text
64 / 529,918 ≈ 0.012%
```

The dataset contains extremely few missing values and is generally well-structured.

---

## Infinite Values

| Column | Infinite Values |
|----------|----------------|
| Flow Bytes/s | 373 |
| Flow Packets/s | 437 |

### Root Cause

The affected rows contained:

```text
Flow Duration = 0
```

Since:

```text
Flow Bytes/s   = Total Bytes   / Flow Duration
Flow Packets/s = Total Packets / Flow Duration
```

division-by-zero produced infinite values.

All occurrences of:

```python
np.inf
-np.inf
```

were converted to:

```python
np.nan
```

to represent undefined numerical values consistently.

---

## Duplicate Rows

- Duplicate rows detected: 26,935
- Percentage of dataset: ~5.08%

### Engineering Decision

Duplicate rows were intentionally retained.

Rationale:

- Network traffic can legitimately produce identical flow patterns.
- Removing duplicates may distort the true distribution of benign and malicious behavior.
- Deduplication decisions should be guided by domain understanding rather than generic preprocessing rules.

Further investigation will be performed during exploratory data analysis.

---

## Column Name Issues

The original dataset contained inconsistent leading spaces:

```text
' Flow Duration'
' Total Fwd Packets'
' Bwd Packet Length Mean'
```

These were standardized using:

```python
df.columns = df.columns.str.strip()
```

This prevents:

- KeyErrors
- Inconsistent feature references
- Visualization issues
- Model pipeline bugs

---

## Encoding Issues

The original dataset contained malformed UTF-8 characters:

```text
Web Attack � Brute Force
Web Attack � XSS
Web Attack � Sql Injection
```

These were normalized during preprocessing to:

```text
Web Attack - Brute Force
Web Attack - XSS
Web Attack - SQL Injection
```

This standardization improves:

- Readability
- Plot labels
- Dashboard consistency
- Model evaluation outputs
- Future maintenance

---

## Monday Dataset Summary

The Monday dataset exhibits excellent overall quality:

- Very few missing values (0.012%)
- Well-understood infinite values
- Consistent schema
- Documented duplicate behavior
- Standardized column naming

The dataset is suitable for exploratory data analysis and downstream machine learning workflows.

---

# Full Dataset Summary

## Combined Dataset

- Total Rows: 2,830,743
- Total Columns: 80
- Memory Usage: 1.99 GB

### Note

The additional column:

```text
Day
```

was introduced during preprocessing to preserve temporal information after combining all datasets.

---

## Temporal Attack Distribution

| Day | Attack Types |
|------|-------------|
| Monday | BENIGN |
| Tuesday | FTP-Patator, SSH-Patator |
| Wednesday | DoS Hulk, DoS GoldenEye, DoS slowloris, DoS Slowhttptest, Heartbleed |
| Thursday Morning | Web Attack - Brute Force, Web Attack - XSS, Web Attack - SQL Injection |
| Thursday Afternoon | Infiltration |
| Friday Morning | Bot |
| Friday Afternoon | PortScan, DDoS |

---

## Engineering Decisions

### Preserve Temporal Information

A new feature:

```text
Day
```

was added to each record before concatenation.

This enables:

- Day-wise exploratory analysis
- Attack timeline visualizations
- Temporal storytelling within the dashboard
- Potential future time-based features

while still supporting a unified machine learning workflow.

---

### Maintain Two Representations

The project maintains two complementary data structures:

```text
daily_dfs
```

Used for:

- Day-specific EDA
- Debugging
- Temporal analysis
- Understanding attack evolution throughout the week

and:

```text
master_df
```

Used for:

- Feature engineering
- Model training
- Model evaluation
- Explainability analysis
- Deployment pipelines

This separation ensures that exploratory requirements and machine learning requirements are both served effectively.

---

### Retain Duplicate Rows

Duplicate network flows were intentionally preserved.

Reasoning:

- Identical network behavior may naturally occur in real systems.
- Removing duplicates could distort attack frequencies.
- Maintaining the original distribution is preferable unless strong evidence suggests data corruption.

---

## Key Takeaways

The CICIDS2017 dataset demonstrates high overall quality:

- Consistent schema across all files.
- Minimal missing data (<0.02%).
- Well-understood infinite values caused by zero-duration flows.
- Human-readable labels after semantic normalization.
- Preserved temporal structure through the `Day` feature.
- Manageable memory requirements (~2 GB RAM) for local experimentation.

The processed dataset is now ready for:

- Exploratory Data Analysis (EDA)
- Feature engineering
- Machine learning model development
- Explainable AI techniques (SHAP)
- Interactive dashboard integration
- Final deployment workflows
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

---

## Infinite Values

| Column | Infinite Values |
|----------|----------------|
| Flow Bytes/s | 373 |
| Flow Packets/s | 437 |

Root cause:

Flow duration equal to zero caused division-by-zero during rate calculations.

All infinite values were converted to `NaN`.

---

## Duplicate Rows

- Duplicate rows detected: 26,935
- Percentage of dataset: ~5.08%

Decision:

Duplicates will be retained for now and investigated further during exploratory data analysis, since repeated network flows may represent legitimate traffic patterns.

---

## Column Name Issues

Leading spaces existed in multiple columns, for example:

```text
' Flow Duration'
' Total Fwd Packets'
```

Fixed using:

```python
df.columns = df.columns.str.strip()
```

---

## Encoding Issues

Observed labels:

- Web Attack � Brute Force
- Web Attack � XSS

Further investigation and normalization will be performed during future cleaning stages.

---

## Summary

The Monday dataset is generally clean:

- Very few missing values (0.012%)
- Infinite values fully understood and handled
- Schema consistency confirmed
- Duplicate rows documented
- Column naming standardized

The dataset is suitable for exploratory data analysis and subsequent machine learning workflows.
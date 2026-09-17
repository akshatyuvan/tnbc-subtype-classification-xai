# Dataset

**The CSV is not committed to this repository.** Download it from the source below
and place it in this directory.

## Source

> Su, Liyang (2025), *Evaluation of Machine Learning Models and SHAP Visualization
> on the Diagnosis of Triple Negative and Non-Triple Negative Breast Cancer*,
> Mendeley Data, V1. doi: 10.17632/xs39gcwsdc.1

https://data.mendeley.com/datasets/xs39gcwsdc/1

| | |
|---|---|
| Depositor | Liyang Su |
| Version | V1 |
| Accessed | 7 December 2025 |
| License | CC BY 4.0 |
| Origin | Quanzhou, Fujian Province, China |
| Records | 855 patients |
| Predictors | 15 |
| Missing values | 0 |

CC BY 4.0 permits reuse with attribution, so no further permission was required
for this secondary analysis.

## Outcome label

The column `cancer` does **not** encode presence or absence of breast cancer. All
855 patients have histologically confirmed breast cancer. The label encodes
subtype, as defined in the data provider's own R script (`code.doc`, shipped with
the deposit):

```r
df$cancer = factor(df$cancer, levels = c(0,1), labels = c('TNBC','non-TNBC'))
```

| Value | Subtype | n |
|---|---|---|
| 0 | TNBC | 241 |
| 1 | non-TNBC | 614 |

The positive class in all reported metrics is non-TNBC (1).

## Known gaps in provenance

The source deposit does not document:

- the reference standard used to assign ER, PR and HER2 status
- the recruitment period
- inclusion and exclusion criteria
- whether imaging features were recorded before the diagnostic reference standard

These gaps are stated in the manuscript and place the study at high risk of bias
in the outcome domain under PROBAST+AI.

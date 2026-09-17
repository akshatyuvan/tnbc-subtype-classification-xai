# Triple-Negative vs Non-Triple-Negative Breast Cancer Subtype Classification

Code accompanying the manuscript *Detection of Triple Negative and Non-Triple
Negative Breast Cancer using XAI Driven Red-Crowned Crane Optimization*,
submitted to **Future Science OA** (Taylor & Francis).

Akshat Yuvan<sup>1</sup>, Simran Singhania<sup>1</sup>, Saikiran Pendem<sup>2</sup>,
Krishnaraj Chadaga<sup>1</sup>

<sup>1</sup> Manipal Institute of Technology, Manipal Academy of Higher Education, Manipal, India
<sup>2</sup> Manipal College of Health Professions, Manipal Academy of Higher Education, Manipal, India

Corresponding author: Krishnaraj Chadaga (krishnaraj.chadaga@manipal.edu)

---

## What this study does

**Subtype classification, not cancer detection.** All 855 patients in the cohort
have histologically confirmed breast cancer. The binary outcome distinguishes
triple-negative breast cancer (TNBC) from non-TNBC:

| Label | Subtype | n | % |
|---|---|---|---|
| 0 | TNBC | 241 | 28.2 |
| 1 | non-TNBC | 614 | 71.8 |

The positive class is non-TNBC. Sensitivity therefore describes identification of
the non-triple-negative subtype; **specificity** describes identification of TNBC,
which is the clinically consequential class.

No-information rate: **0.7193**.

## Pipeline

1. Feature selection — Red-Crowned Crane Optimization (RCCO), compared against
   Boruta as the conventional comparator
2. Class balancing — SMOTE, applied to training folds only
3. Classification — eight classical classifiers and eight transformer
   architectures, all under an identical tuning budget
4. Evaluation — repeated stratified nested cross-validation (5 folds x 2 repeats)
   plus a held-out test set retained for final locked-model assessment
5. Interpretation — SHAP, LIME, PDP/ICE, DiCE, anchor-style rules, residual
   analysis; calibration and decision-curve analysis

## Reproducing the results

```bash
git clone <REPO_URL>
cd <REPO_NAME>
pip install -r requirements.txt
```

Download the dataset from Mendeley Data (see `data/README.md`) and place the CSV
in `data/`. Then run `notebooks/Breast_Cancer_Research_Code.ipynb` top to bottom.

All experiments use a fixed random seed of **42** across NumPy, Python's `random`
module and PyTorch.

### TabPFN access token

TabPFN is accessed through the hosted Prior Labs API and requires a token. The
notebook reads it from Colab Secrets or the `TABPFN_TOKEN` environment variable —
it is never hardcoded. Set it before running:

```bash
export TABPFN_TOKEN="your-token-here"
```

As TabPFN is cloud-hosted and subject to server-side change, exact reproduction of
TabPFN outputs cannot be guaranteed across time. All other results are
deterministic under seed 42.

## Headline results

Held-out test set (n = 171; 48 TNBC / 123 non-TNBC):

| Model | Accuracy | Recall | Specificity | ROC-AUC | MCC |
|---|---|---|---|---|---|
| CatBoost | 0.8070 | 0.8862 | 0.6042 | 0.8614 | 0.5079 |
| Gradient Boosting | 0.8012 | 0.8699 | 0.6250 | 0.8723 | 0.5015 |
| XGBoost | 0.7895 | 0.8862 | 0.5417 | 0.8504 | 0.4541 |
| TabPFN | 0.7895 | 0.9024 | 0.5000 | 0.8789 | 0.4436 |

**Selected model:** RCCO + Gradient Boosting, chosen under a prespecified rule
(best on 4 of 7 metrics under nested cross-validation). The leading ensembles are
statistically indistinguishable — the top pair wins only 3 of 10 outer folds.

The selected model identified **30 of 48 TNBC cases** in the held-out test set.

## Repository layout

```
.
├── README.md
├── requirements.txt
├── data/
│   └── README.md          # dataset provenance and download link (CSV not committed)
└── notebooks/
    └── Breast_Cancer_Research_Code.ipynb
```

## Scope and limitations

This is an internal evaluation of a single retrospective public dataset from one
geographic region. It is not validated for clinical use. External validation on an
independent cohort and prospective evaluation would be required before any
clinical application. See the manuscript's limitations section for the full list.

## Citing

Please cite the manuscript once published. The dataset should be cited separately:

> Su, Liyang (2025), *Evaluation of Machine Learning Models and SHAP Visualization
> on the Diagnosis of Triple Negative and Non-Triple Negative Breast Cancer*,
> Mendeley Data, V1. doi: 10.17632/xs39gcwsdc.1

## License

Code in this repository is released under the MIT License. The dataset is
distributed by its original depositor under CC BY 4.0 and is not redistributed
here.

# Predicting Clinical Endpoints from Microarray Data

**How efficient are models based on microarray gene-expression data, combined with age and gender, at predicting clinical endpoints in neuroblastoma?**

An MSc Bioinformatics project (University of Birmingham, Health Data Analytics). It builds and
compares three machine-learning models that integrate microarray gene expression with age and
gender to predict four clinical outcomes — **INSS stage, high-risk status, disease progression,
and death from disease** — and evaluates how class imbalance and hyperparameter tuning affect
performance. The work follows and extends the comparison framework of Zhang et al. (2015).

## Approach

| Stage | Notebook | What it does |
|-------|----------|--------------|
| 1 | `notebooks/01_eda_and_imputation.ipynb` | EDA of clinical features against each endpoint; missing-value handling; gender encoding; dataframe merging; KNN imputation of the microarray matrix |
| 2 | `notebooks/02_preprocessing_and_clustering.ipynb` | Normalisation and z-score outlier handling; unsupervised pathway — PCA → t-SNE → K-Means clustering to derive patient age-groups |
| 3 | `notebooks/03_supervised_modeling.ipynb` | Supervised modeling — Random Forest, SVM, XGBoost across all four endpoints; GridSearch / RandomizedSearch tuning; class-imbalance handling; accuracy / recall / F1 and ROC-AUC |

> **Note on notebook 03.** The original supervised-modeling notebook was lost (it lived only in a
> local Jupyter directory not captured in backup). Notebook 03 reconstructs that stage to reproduce
> the methodology and results documented in the manuscript; it is not a new analysis. The pipeline
> was validated on a data sample, and reproduces the report's pipeline when run on the full cleaned
> dataset. The original reported metrics are cited from `report/`.

## Results (summary)

As reported in the manuscript (`report/HDA_manuscript.docx`):

- **High Risk** was the most predictable endpoint. Random Forest reached ~0.94 accuracy / ~0.96
  recall; XGBoost performed comparably.
- **XGBoost** was the most reliable model overall (ROC-AUC ≈ 0.72 for INSS Stage 5, ≈ 0.70 for
  Stage 4), though its margin over Random Forest and SVM was modest.
- All models were limited on the **rare INSS stages (2a, 2b, 3)** by severe class imbalance, which
  the report identifies as the principal constraint and the target for resampling or additional
  clinical variables in future work.

## Running it

```bash
conda create -n hda python=3.11 -y && conda activate hda
pip install -r requirements.txt
jupyter notebook
```

Run the notebooks in order (01 → 02 → 03). Notebook 03 expects the cleaned dataset at
`data/merged_clinical_gene_expression_data_cleaned.csv` — see `data/README.md` for how to obtain it
(the matrix is too large to host here).

## Tech stack

Python · pandas · NumPy · scikit-learn · XGBoost · matplotlib · seaborn

## Data

The dataset derives from the neuroblastoma cohort of Zhang et al. (2015), *Genome Biology* 16:133
(DOI [10.1186/s13059-015-0694-x](https://doi.org/10.1186/s13059-015-0694-x)), publicly available
via GEO. The raw and processed matrices are not committed (~272 MB / ~79 MB); see `data/README.md`.

## Author

Ross Gibson — MSc Bioinformatics, University of Birmingham.

## Licence

MIT — see `LICENSE`.

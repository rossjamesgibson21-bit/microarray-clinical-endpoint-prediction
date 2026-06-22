# Data

The microarray + clinical matrices used by these notebooks are **not committed** to the repository
because of their size (raw ~272 MB; cleaned ~79 MB), which exceeds GitHub's per-file limit.

## Source

The dataset derives from the neuroblastoma cohort analysed in:

> Zhang, W., Yu, Y., Hertwig, F. *et al.* (2015). Comparison of RNA-seq and microarray-based models
> for clinical endpoint prediction. *Genome Biology* 16, 133.
> https://doi.org/10.1186/s13059-015-0694-x

The underlying gene-expression and clinical data are publicly available via GEO (see the paper's
data-availability section).

## What the notebooks expect

- `notebooks/01` and `02` build the cleaned, merged matrix from the source data.
- `notebooks/03` loads the cleaned matrix from this folder:

  ```
  data/merged_clinical_gene_expression_data_cleaned.csv
  ```

  (a gzipped `.csv.gz` of the same name is also accepted). Place the file here, or re-generate it by
  running notebooks 01–02, before running notebook 03.

Expected shape: samples × [`ID`, `Gender`, `Age`, `clinico.genetic.subgroup`, `MYCN.status`,
`INSS.Stage`, `HighRisk`, `Progression`, `DeathFromDisease`, + ~38,945 log2 gene-expression columns].

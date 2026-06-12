# Principle Component Analysis
 Application of advanced linear algebra concepts

Principal Component Analysis implemented from first principles (NumPy only) on
Ebola surveillance data from the Democratic Republic of Congo. Built for the
**Advanced Linear Algebra (PCA)** formative assignment.

> No `sklearn`, no `pandas`. Only **NumPy** for the maths and **Matplotlib** for the plots.

---

## What this project does

We take a multi-column epidemic dataset, clean it, and reduce it from **9
numeric features down to 2 principal components** while keeping ~82% of the
information. The full PCA pipeline — standardization, covariance, eigen-
decomposition, sorting, and projection — is written by hand so every step is
visible.

---

## Dataset

**DRC Ebola Outbreak — North Kivu, Ituri & Équateur** (Ministry of Health
surveillance, health-zone level).

| Property | Value |
|---|---|
| Rows | 454 |
| Columns | 12 (8 numeric, 4 non-numeric) |
| Non-numeric columns | `report_date`, `country`, `province`, `health_zone` |
| Missing values | 228 blank cells, scattered across numeric columns |

The dataset meets the assignment requirements: more than 7 columns, real
missing values, and at least one non-numeric column.

**Numeric features used:** `province_code` (label-encoded), `new_confirmed`,
`new_probable`, `confirmed_cases`, `probable_cases`, `confirmed_deaths`,
`total_deaths`, `recovered`, `contacts_followed`.

---

## Repository structure

```
.
├── PCA_DRC_Ebola.ipynb       # the completed, executed notebook (all outputs visible)
├── drc_ebola_outbreak.csv    # the dataset
├── contribution_sheet.pdf    # group contribution sheet (add your filled copy)
└── README.md
```

---

## How to run

The notebook runs top-to-bottom with no changes if the CSV sits in the same
folder.

**Google Colab**
1. Upload `PCA_DRC_Ebola.ipynb` and `drc_ebola_outbreak.csv`.
2. Set `filename` in Step 1 to the path Colab gives the CSV
   (e.g. `/content/drc_ebola_outbreak.csv`).
3. `Runtime → Run all`.

**Locally**
```bash
pip install numpy matplotlib jupyter
jupyter notebook PCA_DRC_Ebola.ipynb
```

---

## Pipeline overview

| Step | What happens |
|---|---|
| 1. Load & clean | Read CSV with the `csv` module, label-encode `province`, turn blanks into `NaN`, then mean-impute |
| 2. Standardize | Scale every feature to mean 0, std 1 (with a divide-by-zero guard) |
| 3. Covariance | Build the feature covariance matrix |
| 4. Eigen-decomposition | `np.linalg.eigh` (matrix is symmetric) |
| 5. Sort | Order eigenvalues/eigenvectors largest-first |
| 6. Project | Multiply standardized data by the top eigenvectors |
| 7. Output | Show the reduced 2-D data |
| 8. Visualize | Before vs. after PCA scatter plots |

---

## Tasks

- **Task 1 — PCA from scratch:** covariance → eigenvalues/eigenvectors →
  projection, all by hand.
- **Task 2 — Dynamic component selection:** components are chosen from the
  cumulative explained-variance curve against an 85% threshold, not picked by
  hand.
- **Task 3 — Performance:** the pipeline is fully vectorized and benchmarked on
  the real dataset and on a ~227,000-row stress copy.

---

## Key results

| Component | Variance explained | Cumulative |
|---|---|---|
| PC1 | ~55.0% | 55.0% |
| PC2 | ~27.1% | 82.1% |
| PC3 | ~9.9% | 92.0% |

- **2 components** capture ~82% of the variance — enough to plot the data on a
  flat scatter.
- The **85% rule** technically needs **3 components**; we keep 2 for the
  visualization and explain the tradeoff in the notebook.
- **Benchmark:** PCA on the full 227k-row stress test runs in roughly **150 ms**.

The before/after plots show the data is only *rotated* by PCA — the clusters
stay intact, just realigned onto the directions of greatest variance.

---

## Tools

`numpy` · `matplotlib`

---

## Authors

Peer Pair 45 — *(add member names here)*

GitHub repo: `https://github.com/<your-username>/<your-repo>` *(replace)*

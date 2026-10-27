# HackBio AI For Genomics

Projects and class notes from the HackBio **AI for Genomics** internship. from an essay on AI in genomics, through exploratory analysis and classical machine learning on a cancer drug-response dataset, to deep-learning image segmentation of brain tumours.

| Stage | Topic | Data | Methods | Main output |
|-------|-------|------|---------|-------------|
| [0](#stage-0--introduction) | Introduction to AI in genomics | – | Python basics, essay writing | Essay + intro script |
| [1](#stage-1--exploratory-analysis-of-cancer-drug-sensitivity-gdsc) | Cancer drug sensitivity: exploratory analysis | GDSC | pandas, seaborn, statistical testing | Analysis report |
| [2](#stage-2--predicting-drug-sensitivity-gdsc) | Cancer drug sensitivity: prediction | GDSC | Random Forest regression & classification | R² 0.78, accuracy 0.94 |
| [3](#stage-3--brain-tumour-segmentation-with-u-net) | Brain tumour segmentation | BraTS 2020 MRI | PyTorch, U-Net | Segmentation model, Dice 0.57 |

## Repository layout

```
AI4Genomics/
├── projects/
│   ├── stageZero/    essay + intro script
│   ├── stageOne/     GDSC exploratory analysis (notebooks, report, figures)
│   ├── stageTwo/     GDSC drug-sensitivity prediction
│   └── stageThree/   BraTS brain tumour segmentation
├── notes/            class notes (regression, random forest, XGBoost, CNNs, tensors, ...)
├── data/             large datasets (not tracked in git)
└── requirement.txt   Python dependencies
```

---

## Stage 0 — Introduction

**Files:** [`projects/stageZero/`](projects/stageZero/)

- [`TEAM  PHENYLALANIN ESSAY.md`](projects/stageZero/TEAM%20%20PHENYLALANIN%20ESSAY.md) — team essay *"Can AI predict your future from your DNA?"*, covering AI applications in genomic risk prediction (variant interpretation, polygenic risk scores, GWAS), current limitations, and ethical concerns.
- [`simple_code.py`](projects/stageZero/simple_code.py) — a short Python introduction script.

## Stage 1 — Exploratory analysis of cancer drug sensitivity (GDSC)

**Files:** [`projects/stageOne/`](projects/stageOne/)

**Goal:** explore the *Genomics of Drug Sensitivity in Cancer* (GDSC) dataset — 162,103 drug-response measurements from 737 cancer cell lines and 246 drugs — and find what drives differences in drug response.

**What was done**
- Data cleaning: checked missing values, standardised the genomic flags (CNA, gene expression, methylation), and investigated 4,290 duplicated cell-line/drug pairs.
- Distributions of the response measures (LN_IC50, AUC, Z_SCORE) and of categorical variables.
- Ranked drugs by potency (median LN_IC50) and by how variable their response is across cell lines.
- Compared sensitivity across cancer types, including drug–cancer heatmaps.
- Tested whether copy-number, gene-expression and methylation status are associated with drug response (t-tests, volcano plots).

**Key finding:** drug response is highly heterogeneous across drugs, cell lines and cancer types; gene expression was the molecular feature most often associated with sensitivity, while copy-number and methylation had more selective effects.

**Outputs:** [`notebook/notebook.ipynb`](projects/stageOne/notebook/notebook.ipynb) (analysis), [`notebook/data_exp.ipynb`](projects/stageOne/notebook/data_exp.ipynb) (data exploration), and the written reports [`report/GDSC_Analysis_Report.md`](projects/stageOne/report/GDSC_Analysis_Report.md) and [`report/submission.md`](projects/stageOne/report/submission.md).

## Stage 2 — Predicting drug sensitivity (GDSC)

**Files:** [`projects/stageTwo/`](projects/stageTwo/)

**Goal:** using the same GDSC data, build machine-learning models that predict how sensitive a cancer cell line is to a drug, based on `LN_IC50`.

**What was done**
- Encoded categorical features (drug, target pathway, cancer type, MSI status, growth properties, genomic flags) and used an 80/20 train/test split.
- Excluded **AUC** and **Z_SCORE** to avoid data leakage. Both come from the same dose-response curve as LN_IC50, so including them pushed R² to 0.97 without the model learning anything useful.
- **Regression** — Random Forest predicting the exact LN_IC50 value (evaluated with R², RMSE, MAE).
- **Classification** — LN_IC50 split into *Sensitive* (bottom 25%) and *Resistant* (top 25%), with the ambiguous middle 50% removed; Random Forest classifier evaluated with accuracy, precision/recall and a confusion matrix.
- Feature-importance analysis and biological interpretation of the results, plus a discussion of limitations (cell lines vs patients, 2D culture, single-agent screening).

| Notebook | Model | Result |
|----------|-------|--------|
| [`notebook.ipynb`](projects/stageTwo/notebook.ipynb) | Random Forest regression | R² = 0.78, RMSE = 1.34 |
| [`notebook.ipynb`](projects/stageTwo/notebook.ipynb) | Random Forest classification | Accuracy = 0.94 |
| [`drug_sensitivity.ipynb`](projects/stageTwo/drug_sensitivity.ipynb) | Random Forest regression (tuned) | R² = 0.77, RMSE = 1.36 |
| both | Baseline: each drug's average LN_IC50 | R² = 0.72 |

Drug identity and target pathway are the most important features, followed by cancer type and growth properties. The baseline shows that most of the predictive power comes from how potent each drug is overall. Predicting which individual cell lines respond to a given drug would need real molecular measurements, such as gene expression or mutations; this dataset only records whether those data exist.

## Stage 3 — Brain tumour segmentation with U-Net

**Files:** [`projects/stageThree/brain_tumor_segmentation.ipynb`](projects/stageThree/brain_tumor_segmentation.ipynb)

**Goal:** build a complete medical image segmentation pipeline from scratch: train a U-Net that takes an MRI slice and outputs a mask marking where the tumour is.

**Data:** BraTS 2020 training data, stored as 57,198 2D slices in `.h5` files. Each slice has 4 MRI modalities (240×240×4) and a 3-class tumour mask (240×240×3).

**Pipeline**
1. **Data preparation** — a PyTorch `Dataset` that uses the FLAIR channel, applies min-max normalisation, and merges the three tumour classes into one binary mask. Slices without tumour are dropped (24,422 remain), and a random 3,000-slice subset is split 85/15 into training and validation sets.
2. **Model** — a U-Net with an encoder, a bottleneck, a decoder with skip connections and a 1×1 output layer (32→512 channels, 7.8M parameters).
3. **Training** — binary cross-entropy loss (`BCEWithLogitsLoss`) and Adam (lr 1e-3) for 5 epochs on the Apple Silicon GPU, tracking training and validation loss, Dice and IoU each epoch.
4. **Evaluation and visualisation** — Dice and IoU on the validation set, loss curves, and MRI / ground truth / prediction comparisons.

**Results (validation set, best epoch)**

| Metric | Score |
|--------|-------|
| Dice | 0.571 |
| IoU | 0.470 |

**Limitations:** trained on only a subset of the data for a few epochs, uses FLAIR only, and splits by slice rather than by patient. More data, all four modalities, a Dice-based loss, augmentation and a patient-level split are the natural next steps.

**Running it:** the notebook expects the dataset at `data/brats2020/BraTS2020_training_data/content/data/`. On the first run it scans all slices and caches the list of tumour-containing files in `valid_files.txt`.

---

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirement.txt
```

The GDSC spreadsheet is included in `projects/stageOne/data/` and `projects/stageTwo/data/`. The BraTS 2020 dataset is too large for git; download it separately into `data/brats2020/`.

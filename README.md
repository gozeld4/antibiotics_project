# Antibiotic Synergy Prediction

A machine learning project for predicting synergistic effects of antibiotic combinations against bacterial pathogens, using molecular fingerprints and transformer-based embeddings.

## Overview

This project builds and evaluates multiple ML models to classify whether antibiotic–compound combinations produce synergy, and to regress continuous synergy scores (Bliss independence). It covers the full pipeline: molecular encoding, feature engineering, model training, cross-validation, and evaluation.

## Data

| Dataset | Description |
|---|---|
| `A_blissind_abxinfo_DropArray.xlsx` | Core dataset with antibiotic metadata and Bliss independence scores |
| `v2_all_data_embedded.csv` | ~1.3M samples with ChemBERTa fingerprint embeddings |
| `7k_onehot_and_smiles.csv` | ~7,000 samples with one-hot features and SMILES strings |
| `all_synergy_labeled.csv` | Binary synergy labels (synergistic / non-synergistic) |
| `all_data_clean.csv` | Cleaned dataset used for training |

**Features:** Morgan fingerprints (ECFP, 1024-bit, radius 2), ChemBERTa embeddings (199- and 768-dim), antibiotic concentration, Bliss scores (Ea_med, Ec_med), bacterial strain one-hot encoding (Ab17978, AbLac4, Kp0087, Kp43816, PAO1, Pa0095).

## Methods

### Molecular Encoding
- **Morgan Fingerprints (ECFP)** via RDKit — 1024 bits, radius 2
- **ChemBERTa Embeddings** — pre-trained `ChemBERTa-77M-MTR` transformer model via Hugging Face

### Models

**Classification** (5-fold cross-validation):
- LightGBM
- XGBoost
- Random Forest
- Logistic Regression
- MLP Neural Network (custom PyTorch implementation with batch norm, dropout, early stopping)

**Regression:**
- XGBoost Regressor — predicts continuous Bliss independence scores

### Evaluation Metrics
- Classification: AUROC, accuracy, confusion matrix, ROC curves
- Regression: R², MSE, MAE

## Results

Models are compared across three dataset variants:
- **7k dataset** with ChemBERTa embeddings (~440 features)
- **Balanced 2k/2k dataset** — equal synergistic/non-synergistic samples to address class imbalance
- **Full embedded dataset** (~1.3M samples)

Visualizations include ROC curves, confusion matrices, XGBoost prediction vs. actual scatter plots, and feature importance plots.

## Tech Stack

| Category | Libraries |
|---|---|
| Data | pandas, numpy |
| Visualization | matplotlib, seaborn |
| ML | scikit-learn, XGBoost, LightGBM |
| Deep Learning | PyTorch, torch_geometric |
| Chemistry | RDKit, Hugging Face Transformers (ChemBERTa) |
| Utilities | tqdm, Google Colab |

## Project Structure

```
antibiotics_project/
├── Master_sheet_Antibiotics_project.ipynb   # Main analysis notebook
└── README.md
```

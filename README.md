# LNP Stability Predictions

Data and code for the manuscript **"Machine learning predicts differences in the stability of lipid nanoparticles encapsulating mRNA or siRNA"** (Tynes, Shrivastava, Song).

An XGBoost classifier predicts the formation of stable four-component lipid nanoparticles (LNPs) from molecular descriptors (Mordred) and quantum-chemical interaction energies (SAPT0 via AP-Net). Models are trained per nucleic acid payload (mRNA, siRNA, and combined RNA) and validated on clinically relevant COVID-19 vaccine LNP chemistries (SM-102, ALC-0315).

## Dependencies

This project uses Python 3 and requires up-to-date versions of the following Python packages:
* numpy
* scipy
* pandas
* xgboost
* sckit-learn
* imbalanced-learn
* rdkit
* mordred
* tensorflow
* matplotlib

## Quick start

```bash
# Produce processed_data.csv and per-payload splits from raw data
python models/preprocess.py

# Train and test each model
python models/LNP_model.py
```
# LNP Stability Predictions

This repository contains code and data associated with the manuscript, **"Machine learning predicts differences in the stability of lipid nanoparticles encapsulating mRNA or siRNA"** (Tynes, Shrivastava, and Song). The study predicts the formation of stable four-component lipid nanoparticles with gradient boosted decision trees, integrated with modred molecular descriptors to encode chemical properties and SAPT0 lipomer-cholesterol quantum- chemical interaction energies computed with AP-Net. Models are trained on nucleic acid payload specific datasets and validated on clinically relevant COVID-19 vaccine LNP chemistries.

## Dependencies

This project uses Python 3 and requires up-to-date versions of the following Python packages:
* numpy
* scipy
* pandas
* xgboost
* scikit-learn
* imbalanced-learn
* rdkit
* mordred
* tensorflow
* matplotlib

## Data

Original LNP screening data is stored in 'datasets/raw_data.csv', with one row per LNP formulation and a label indicating a LNP as unstable or stable.

Engineered features are stored in 'dataesets/processed_data.csv', with five SAPT0 energy features and approximately 6000 Mordred descriptors corresponding to component type. Payload specific 80/20 splits are stored in 'datasets/{mRNA,siRNA,RNA}\_{train,test}.csv'.

Stretched energy minimized lipid conformations used as input to AP-Net are stored in 'datasets/mol_conformation/'. SAPT0 energies predicted with AP-Net are stored in 'datasets/dimer_interactions_stretch.pkl' for training and 'datasets/dimer_interactions_pfizer_moderna.pkl' for the Figure 4 validation. AP-Net source code and pretrained models are in 'AP-Net-master/'.

## Preprocessing

The script 'models/preprocess.py' combines SMILES strings, inferred AP-Net SAPT energies, and calculated Mordred descriptors with the molecular composition and mass ratio, then splits into payload specific datasets for mRNA, siRNA, and combined RNA train/test sets.

```bash
python models/preprocess.py
```

## Training and inference
 
The script `models/LNP_model.py` runs a 100 iteration random hyperparameter search with 5-fold cross-validation, trains a final XGBoost model with the best parameters, and scores the held-out test set. Set `model_name` to `'mRNA'`, `'siRNA'`, or `'RNA'` at the beginning of the file. The script loads tuned hyperparameters from `models/params/` to reproduce the models reported in the paper.
 
```
python models/LNP_model.py
```

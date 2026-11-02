# Project Methodology

## 1. Research Objective

This project explores cross-dataset cell representation learning using PBMC3k and PBMC10k single-cell RNA sequencing datasets. The goal is to investigate cell clustering, label transfer, and low-dimensional representation learning.

## 2. Dataset Description

- **PBMC3k:** Used as the reference dataset for exploratory clustering and classifier training.
- **PBMC10k:** Used as the query dataset for transferred label analysis and independent clustering.

Both datasets contain gene expression measurements from peripheral blood mononuclear cells.

## 3. Quality Control

Cells were filtered using:
- Minimum number of detected genes: 200
- Maximum number of detected genes: 5,000 for PBMC10k
- Mitochondrial gene percentage threshold: 15% for PBMC10k

Quality control thresholds were selected for exploratory analysis.

## 4. Preprocessing

The following steps were applied:
1. Total-count normalization to 10,000 counts per cell.
2. Logarithmic transformation using `log1p`.
3. Selection of 2,000 highly variable genes from PBMC3k.
4. Feature alignment between the datasets.

## 5. Clustering and Visualization

PCA was used for dimensionality reduction. Neighborhood graphs were constructed, followed by Leiden clustering. UMAP was used to visualize cell populations.

## 6. Label Transfer

A Logistic Regression classifier was trained on PBMC3k cluster labels using a stratified train-test split.

The trained classifier was then used to predict cluster labels for PBMC10k.

## 7. Representation Learning

A neural network autoencoder was implemented using PyTorch.

Architecture:

- Input layer: 2,000 features
- Encoder: 2,000 → 512 → 128 → 64
- Latent representation: 64 dimensions
- Decoder: 64 → 128 → 512 → 2,000

The model was trained using Mean Squared Error (MSE) loss and the Adam optimizer for 10 epochs.

## 8. Evaluation Metrics

- Accuracy
- Macro F1-score
- Weighted F1-score
- Adjusted Rand Index (ARI)
- Normalized Mutual Information (NMI)
- Reconstruction Mean Squared Error

## 9. Limitations

This study is preliminary and exploratory.

The classifier evaluation uses a random split within PBMC3k. It does not represent a fully held-out cross-dataset evaluation. The autoencoder was trained on the combined datasets, so its embeddings do not establish generalization to an unseen dataset.

Cell annotations are provisional and require further biological validation.

## 10. Future Work

- Perform rigorous cross-dataset validation.
- Explore batch-effect correction techniques.
- Investigate advanced cell representation learning methods.
- Improve biological cell-type annotation.
- Evaluate representations using additional biological metrics.

# Cross-Dataset Cell Representation Learning for Biomedical Discovery

## Overview

This project explores cross-dataset cell representation learning using single-cell RNA sequencing (scRNA-seq) data. The objective is to investigate whether machine learning models can learn meaningful cell representations across different datasets and support biomedical discovery.

The project uses PBMC3k and PBMC10k datasets for exploratory analysis, cell clustering, label transfer, and representation learning.

## Objectives

- Explore and preprocess single-cell RNA-seq datasets.
- Identify highly variable genes and meaningful cell clusters.
- Investigate cross-dataset cell label transfer.
- Learn low-dimensional cell representations using an autoencoder.
- Compare transferred labels with independently generated clusters.
- Visualize cell populations and learned embeddings.

## Datasets

| Dataset | Description |
|---|---|
| PBMC3k | Peripheral blood mononuclear cells dataset containing approximately 3,000 cells |
| PBMC10k | Peripheral blood mononuclear cells dataset containing approximately 10,000 cells |

Data are obtained using Scanpy's single-cell analysis workflows and 10x Genomics data.

## Methodology

1. **Quality Control:** Filter cells based on gene counts and mitochondrial gene percentage.
2. **Normalization:** Normalize total counts and apply log transformation.
3. **Feature Selection:** Select 2,000 highly variable genes using PBMC3k as the reference.
4. **Dimensionality Reduction:** Apply PCA and UMAP.
5. **Clustering:** Perform Leiden clustering to identify cell populations.
6. **Cell Label Transfer:** Train a Logistic Regression classifier on PBMC3k and transfer labels to PBMC10k.
7. **Representation Learning:** Train a neural network autoencoder to learn 64-dimensional cell embeddings.
8. **Evaluation:** Explore classification performance, clustering agreement, and reconstruction error.

## Preliminary Results

### PBMC3k Cell Clustering

Six clusters were identified using Leiden clustering. Preliminary marker-based annotations suggested the presence of T cells, B cells, monocytes, NK-like cells, dendritic/myeloid-like cells, and platelets.

### Label Transfer

The Logistic Regression classifier achieved the following results on a stratified held-out PBMC3k test split:

| Metric | Score |
|---|---:|
| Accuracy | 0.9754 |
| Macro F1-score | 0.9436 |
| Weighted F1-score | 0.9755 |

The comparison between transferred labels and independently generated PBMC10k clusters yielded:

| Metric | Score |
|---|---:

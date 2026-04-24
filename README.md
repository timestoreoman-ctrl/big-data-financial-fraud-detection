# Scalable Graph-Based Financial Fraud Detection on Elliptic++

This repository contains the implementation notebook for a Big Data course project on scalable graph-based financial fraud detection using the full Elliptic++ Actors Dataset.

## Project Overview

The goal of this project is to detect illicit Bitcoin wallet addresses using large-scale transaction graph data. The project processes wallet features, wallet class labels, and address-address graph edges using PySpark on Google Colab, extracts graph-based degree features, trains machine learning models, and evaluates both predictive performance and processing efficiency.

## Tools and Environment

- Google Colab
- PySpark
- Spark MLlib
- Python
- Pandas
- Matplotlib

## Dataset

The project uses the full Elliptic++ Actors Dataset, including:

- `wallets_features.csv`
- `wallets_classes.csv`
- `AddrAddr_edgelist.csv`
- `AddrTx_edgelist.csv`
- `TxAddr_edgelist.csv`

Dataset source:  
https://github.com/git-disl/EllipticPlusPlus

The dataset files are not uploaded to this repository because of their large size. The notebook downloads or reads the dataset from the official source / Google Drive.

## Methodology

The implementation follows these main steps:

1. Prepare the Google Colab and PySpark environment.
2. Download the full Elliptic++ Actors Dataset.
3. Load the full CSV files using PySpark.
4. Convert CSV files to Parquet format for more efficient processing.
5. Merge wallet features with wallet class labels.
6. Analyze class imbalance between licit and illicit wallets.
7. Extract graph-based features from the address-address edge list:
   - in-degree
   - out-degree
   - total degree
   - in/out ratio
8. Train and evaluate machine learning models:
   - Logistic Regression with original features
   - Logistic Regression with graph-enhanced features
   - Random Forest with graph-enhanced features
9. Measure processing time, speedup, and efficiency for graph feature extraction.
10. Generate final tables and figures for the research paper.

## Results Summary

The Graph-Enhanced Random Forest achieved the best overall predictive performance:

| Model | Accuracy | ROC-AUC | PR-AUC | Fraud Precision | Fraud Recall | Fraud F1 |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression - Original Features | 0.5566 | 0.7321 | 0.1738 | 0.0938 | 0.8348 | 0.1687 |
| Logistic Regression - Graph Features | 0.5549 | 0.7326 | 0.1704 | 0.0934 | 0.8338 | 0.1680 |
| Random Forest - Graph Features | 0.8937 | 0.8482 | 0.4192 | 0.2591 | 0.5236 | 0.3467 |

## Speedup and Efficiency

Processing time, speedup, and efficiency were measured for graph degree feature extraction on the full address-address edge list. The experiments were executed in Google Colab using Spark local mode. Since Colab is not a true multi-node Spark cluster, Spark overhead and shuffle costs affected the measured speedup. These limitations are discussed in the research paper.

## Repository Contents

- `Financial_Fraud_Detection_EllipticPlusPlus_BigData.ipynb`  
  Main implementation notebook.

- `README.md`  
  Project description and summary.

## Notes

This project was developed for the Big Data course (ICTS 6339). The implementation focuses on full-dataset processing, graph-based feature engineering, model evaluation, and system-level timing analysis.

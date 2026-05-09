أكيد، هذا **README.md كامل** جاهز تنسخيه وتحطيه بدل الموجود كاملًا في GitHub:

```markdown
# Scalable Graph-Based Financial Fraud Detection on Elliptic++

This repository contains the implementation notebook for a Big Data course project on scalable graph-based financial fraud detection using the full Elliptic++ Actors Dataset.

## Project Overview

The goal of this project is to detect illicit Bitcoin wallet addresses using large-scale transaction graph data. The project processes wallet-level actor features, wallet labels, and address-address graph edges using PySpark. It applies graph-based degree features, trains machine learning models, and evaluates both predictive performance and processing efficiency.

## Tools and Environment

- Google Colab
- PySpark
- Spark ML
- Spark local[*]
- Spark Standalone Mode
- One Spark Master process
- Four Spark Worker JVM processes
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

The dataset files are not uploaded to this repository because of their large size. The notebook downloads or reads the dataset from the official source / Google Drive path.

## Methodology

The implementation follows these main steps:

1. Prepare the Google Colab and PySpark environment.
2. Download the full Elliptic++ Actors Dataset.
3. Load the full CSV files using PySpark.
4. Convert CSV files to Parquet format for more efficient processing.
5. Merge wallet features with wallet class labels.
6. Assign class labels between licit and illicit wallets.
7. Extract graph-based features from the address-address edge list:
   - in-degree
   - out-degree
   - total degree
   - in/out ratio
8. Join graph features with the known supervised wallet records.
9. Apply a chronological train/test split using the Time step column.
10. Train and evaluate the implemented Spark ML models:
    - Logistic Regression with original features
    - Logistic Regression with graph-enhanced features
    - Random Forest with graph-enhanced features
11. Measure prediction metrics, speedup, and efficiency for graph feature extraction.
12. Run Spark Standalone Mode locally using one Spark Master and four Worker JVM processes.
13. Compare Spark Standalone partition results using 1, 2, 4, and 8 partitions.

## Implemented Models

Only the models actually trained in the notebook are reported as implemented models:

| Model | Input Features | Implemented? |
|---|---|---|
| Logistic Regression - Original Features | 56 original wallet features | Yes |
| Logistic Regression - Graph Features | 56 original features + 4 degree features | Yes |
| Random Forest - Graph Features | 56 original features + 4 degree features | Yes |
| Temporal GNN / STGNN-FD | Temporal event histories and neighborhoods | No, future work only |

Temporal GNN models such as TGN, TGAT, GCN, GAT, and GraphSAGE were not trained in this notebook. They are discussed only as related work or future work.

## Result Summary

The Graph-Enhanced Random Forest achieved the best overall predictive performance.

| Model | Accuracy | ROC-AUC | PR-AUC | Fraud Precision | Fraud Recall | Fraud F1 |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression - Original Features | 0.5566 | 0.7321 | 0.1738 | 0.0938 | 0.8348 | 0.1687 |
| Logistic Regression - Graph Features | 0.5549 | 0.7326 | 0.1704 | 0.0934 | 0.8338 | 0.1680 |
| Random Forest - Graph Features | 0.8937 | 0.8482 | 0.4192 | 0.2591 | 0.5236 | 0.3467 |

## Speedup and Efficiency

Sequential Python degree extraction was compared with PySpark local[*] degree extraction.

| Execution Setting | Runtime | Speedup | Efficiency |
|---|---:|---:|---:|
| Sequential Python baseline | 9.1181 s | 1.0000x | 1.0000 |
| PySpark local[*] | 13.5466 s | 0.6731x | 0.0841 |
| Spark single partition | 11.2927 s | 1.0000x | 1.0000 |
| Spark 8 partitions | 18.6112 s | 0.6068x | 0.0758 |

For the tested graph-degree extraction workload, Spark local[*] was slower than the sequential Python baseline in the Google Colab environment. This does not mean that Spark is ineffective for Big Data, but it shows the overhead of local Spark execution, scheduling, repartitioning, and shuffle costs.

## Spark Standalone Experiment

In addition to the previous Spark local[*] experiment, a Spark Standalone experiment was executed locally on the same Google Colab machine. The setup used one Spark Master process and four Spark Worker JVM processes. This setup is not a physical multi-node cluster, but it follows the Spark Standalone execution model more closely than local[*].

The same AddrAddr_edgelist degree-extraction task was tested using 1, 2, 4, and 8 Spark partitions. The standalone results showed that increasing the number of partitions did not improve runtime in the local Colab environment, mainly because of Spark overhead, worker communication cost, and shuffle cost.

| Execution Setting | Runtime | Speedup | Efficiency |
|---|---:|---:|---:|
| Spark Standalone 1 partition | 25.5570 s | 1.0000x | 1.0000 |
| Spark Standalone 2 partitions | 63.7371 s | 0.4010x | 0.2005 |
| Spark Standalone 4 partitions | 39.8322 s | 0.6416x | 0.1604 |
| Spark Standalone 8 partitions | 33.7050 s | 0.7583x | 0.0948 |

All Spark Standalone runs produced the same number of unique graph-degree nodes: 822,942.

## Repository Contents

- `financial_fraud_detection.ipynb`  
  Main implementation notebook.

- `README.md`  
  Project description and summary.

## Notes

This project was developed for the Big Data course ICTS 6339. The implementation focuses on full-dataset processing, graph-based feature engineering, model evaluation, and system-level timing analysis.

The project does not claim to implement a true temporal GNN. Temporal GNN models are treated as future work.

## Main Limitations

- The Spark Standalone experiment was executed on one Google Colab machine, not on a real physical multi-node cluster.
- Exact hardware details such as CPU, RAM, and OS were not printed in the notebook.
- A full column-wise missing-value audit was not printed in the notebook.
- Temporal GNN models were not trained.
```

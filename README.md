# Customer Segmentation Using DBSCAN

## Project Overview

This project applies the **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** algorithm to segment mall customers based on their **Annual Income** and **Spending Score** using **Weka 3.9.6**.

## Problem Statement

The objective of this project is to segment mall customers based on their annual income and spending behavior using the DBSCAN density-based clustering algorithm in Weka. The algorithm identifies dense groups of customers and detects noise or outlier customers without requiring the number of clusters to be specified in advance.

## Dataset

* **Name:** Mall Customers Dataset
* **Instances:** 200
* **Attributes Used:** Annual Income (k$), Spending Score (1-100)

| Attribute              | Description                           |
| ---------------------- | ------------------------------------- |
| CustomerID             | Unique customer identifier            |
| Genre                  | Male/Female                           |
| Age                    | Customer's age in years               |
| Annual Income (k$)     | Annual income in thousands of dollars |
| Spending Score (1-100) | Spending score assigned by the mall   |

## Algorithm: DBSCAN

DBSCAN is a density-based clustering algorithm that:

* Does **not** require the number of clusters (K) to be specified in advance
* Discovers clusters based on data density
* Automatically identifies **noise/outlier** points
* Can find clusters of **arbitrary shape**

### Parameters

| Parameter   | Value | Description                           |
| ----------- | ----- | ------------------------------------- |
| Epsilon (ε) | 0.06  | Radius of neighborhood around a point |
| MinPts      | 5     | Minimum points to form a dense region |

## Project Workflow

```text
Mall Customers Dataset (CSV)
         ↓
Data Preprocessing (Remove unnecessary attributes)
         ↓
Normalization (Scale to 0-1 range)
         ↓
Apply DBSCAN (ε=0.06, MinPts=5)
         ↓
5 Customer Clusters + 21 Noise Points
         ↓
Interpret Customer Segments
```

## Results

### Clustering Output

| Cluster | Instances | Percentage | Segment Name        |
| ------- | --------- | ---------- | ------------------- |
| 0       | 71        | 40%        | High Spenders       |
| 1       | 85        | 47%        | Low Spenders        |
| 2       | 7         | 4%         | Ultra High Spenders |
| 3       | 5         | 3%         | Ultra Low Spenders  |
| 4       | 11        | 6%         | Moderate Spenders   |
| Noise   | 21        | 11%        | Outlier Customers   |

### Parameter Experiments

| Epsilon  | MinPts | Normalized? | Clusters | Noise  | Observation                     |
| -------- | ------ | ----------- | -------- | ------ | ------------------------------- |
| 9.0      | 5      | No          | 1        | 0      | All points merged — ε too large |
| 0.12     | 5      | Yes         | 3        | 0      | Only spending-based split       |
| 0.08     | 5      | Yes         | 3        | 12     | Some noise, only 3 clusters     |
| **0.06** | **5**  | **Yes**     | **5**    | **21** | **Best result**                 |

### DBSCAN vs K-Means

| Feature            | DBSCAN                   | K-Means        |
| ------------------ | ------------------------ | -------------- |
| Number of clusters | Discovered automatically | Must specify K |
| Noise detection    | ✅ Yes (21 outliers)      | ❌ No           |
| Small clusters     | ✅ Found (7, 5, 11)       | ❌ Minimum = 29 |
| Cluster shape      | Any shape                | Spherical only |

## Tools Used

* **Weka 3.9.6** — Machine learning workbench
* **optics_dbScan** — DBSCAN package for Weka
* **Normalize Filter** — weka.filters.unsupervised.attribute.Normalize

## Business Applications

* **Targeted Marketing** — Different campaigns for each segment
* **Outlier Detection** — Investigate 21 unusual customers individually
* **Customer Retention** — Focus on High Spenders to prevent churn
* **VIP Programs** — Exclusive benefits for Ultra High Spenders
* **Growth Strategy** — Promotions to move Low Spenders to higher segments

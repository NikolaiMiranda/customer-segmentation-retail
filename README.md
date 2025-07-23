# customer-segmentation-retail
# Customer Segmentation using RFM and K-Means

This project performs **customer segmentation analysis** on an e-commerce dataset using two techniques:

- **RFM Analysis** (Recency, Frequency, Monetary)
- **K-Means Clustering**

The goal is to identify distinct customer groups based on purchasing behavior to inform targeted marketing strategies.

---

## Dataset

The analysis uses the `online_retail.csv` dataset, which contains transactional data from a UK-based online retail store.

---

## Methodology

### 1. Data Loading and Preprocessing

- Load the dataset into a pandas DataFrame.
- Remove rows with missing `CustomerID`.
- Exclude cancelled orders (invoices starting with `'C'`).
- Create a `Revenue` column: `Quantity × UnitPrice`.

---

### 2. RFM Analysis

- **RFM Score Calculation**:
  - **Recency**: Days since the customer’s last purchase.
  - **Frequency**: Number of unique invoices per customer.
  - **Monetary**: Total revenue from each customer.

- **Quantile-Based Scoring**:
  - RFM values are scored from 1–4 (quartiles).
  - Recency is reversed (lower days = higher score).

- **Segment Creation**:
  - Combine R, F, and M scores into a segment (e.g., `444`, `123`).
  - Map RFM segments to labels: _Champions_, _Loyal_, _Lost_, etc.

- **Analysis**:
  - Visualize distribution of segments.
  - Calculate average RFM values per segment.

---

### 3. K-Means Clustering

- **Feature Scaling**:
  - Standardize RFM values using `StandardScaler`.

- **Optimal Clusters**:
  - Use the Elbow Method to identify the best number of clusters (K).

- **Clustering**:
  - Apply K-Means on scaled RFM data.
  - Assign cluster labels to customers.

- **Cluster Analysis**:
  - Analyze average unscaled RFM values per cluster.
  - Assign descriptive names (e.g., `Loyalists`, `At-Risk`, `Lost`).
  - Visualize customer distribution across clusters.

---

## Visualizations

The project includes several visualizations to help understand the data and the segmentation results:

- **Distribution of RFM Metrics**:
  - Histograms of Recency, Frequency, and Monetary values.

- **RFM Segment Distribution**:
  - Bar plot of customer counts in each RFM level.

- **Elbow Method Plot**:
  - Line plot of WCSS vs. number of clusters.

- **K-Means Cluster Distribution**:
  - Bar plot showing customer counts per K-Means cluster.

> **Note**: Replace `path/to/your/your_plot_name.png` with the actual path to your saved plot images in the repository.

---

## Findings

The analysis reveals distinct customer segments:

### RFM Segmentation:
- **Champions / Loyal**: High scores in Recency, Frequency, and Monetary.
- **At-Risk / Lost**: Low RFM scores, indicating inactivity or churn risk.

### K-Means Clustering (K = 3):

- **Loyalists (Cluster 2)**: High frequency and monetary, low recency.
- **At-Risk (Cluster 0)**: Moderate on all metrics.
- **Lost (Cluster 1)**: High recency, low frequency and monetary.

Both techniques support targeted marketing by highlighting customer value and retention priorities.

---

## Code Structure

- Implemented in a Google Colab / Jupyter Notebook.
- Libraries used: `pandas`, `matplotlib`, `seaborn`, `sklearn`.
- Each cell corresponds to a step in the workflow (loading, cleaning, analysis, visualization).

---

## How to Use

1. Clone this repository.
2. Ensure `online_retail.csv` is in the project directory.
3. Open the notebook in Colab or Jupyter.
4. Run cells sequentially to reproduce the analysis.
5. Save generated plots and update image paths in the README if needed.

---

## Future Work

- Explore alternative clustering algorithms (e.g., DBSCAN, Hierarchical Clustering).
- Implement more granular RFM strategies.
- Build targeted marketing campaigns.
- Perform product-level analysis within each customer segment.

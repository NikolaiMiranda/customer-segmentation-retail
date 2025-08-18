# Customer Segmentation with K-Means Clustering

This project demonstrates an end-to-end process for segmenting customers using transactional retail data from the UCI Online Retail Dataset. The workflow includes data collection, cleaning, feature engineering, clustering with K-Means, and interactive visualization of customer segments. The goal is to identify distinct customer groups based on purchasing behavior to inform marketing strategies and enhance customer relationship management.

## Table of Contents
- [Skills Demonstrated](#skills-demonstrated)
- [Dependencies](#dependencies)
- [Data Gathering and Cleaning](#data-gathering-and-cleaning)
- [Handling Cancelled Orders (Data Cleaning Challenge)](#handling-cancelled-orders-data-cleaning-challenge)
- [Feature Engineering](#feature-engineering)
- [Customer Segmentation with K-Means](#customer-segmentation-with-k-means)
- [Cluster Analysis](#cluster-analysis)
- [Marketing Strategies Based on Customer Segmentation](#marketing-strategies-based-on-customer-segmentation)
- [Segmentation Visualizations](#segmentation-visualizations)
- [Key Results](#key-results)
- [Acknowledgments](#acknowledgments)

## Skills Demonstrated
- **Python**: Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Plotly
- **Data Wrangling**: Handling missing values, cleaning cancellations, and removing outliers
- **Feature Engineering**: RFM (Recency, Frequency, Monetary) and behavioral features
- **Unsupervised Machine Learning**: K-Means clustering, Elbow Method, Davies-Bouldin Index
- **Data Visualization**: Interactive dashboards and 3D PCA scatter plots with Plotly
- **Business Insight Generation**: Translating cluster outputs into meaningful customer segments

## Dependencies
To run this project, install the following Python packages:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn plotly ucimlrepo
```

## Data Gathering and Cleaning
- **Dataset**: UCI Online Retail Dataset (ucimlrepo, dataset ID 352)
- Joined IDs and features tables into a single DataFrame
- Handled missing values by dropping rows without CustomerID
- Removed canceled orders by matching against originals and adjusting quantities
- Filtered out invalid transactions (e.g., UnitPrice = 0)

## Handling Cancelled Orders (Data Cleaning Challenge)
One of the most significant challenges in this dataset was dealing with canceled transactions. In the raw data, cancellations are logged as separate invoices prefixed with "C", which can distort customer purchase behavior if not properly reconciled.

### Approach
A custom function `remove_cancellations(df)` was implemented to systematically adjust the dataset:
1. Separated cancellations and original transactions by checking if InvoiceNo started with "C".
2. Converted cancellation quantities to absolute values for subtraction from original order quantities.
3. Grouped cancellations across multiple records by key identifiers (StockCode, Description, UnitPrice, CustomerID, and Country) to aggregate all cancellations for the same item and customer.
4. Merged grouped cancellations back into the original dataset on those identifiers.
5. Adjusted original quantities by subtracting cancellation totals (`Quantity - Quantity_cancel`).
6. Removed rows with zero or negative quantities to exclude canceled purchases.

### Why It Matters
Without this step, canceled items would inflate key metrics like Monetary Value, Frequency, and Quantity, leading to misleading RFM scores and cluster assignments. This reconciliation ensures the dataset reflects true customer purchasing behavior, providing a clean foundation for segmentation and marketing strategy.

## Feature Engineering
Engineered customer-level features to capture purchasing behavior:
- **Recency**: Days since last purchase
- **Frequency**: Number of unique invoices
- **Monetary**: Total spend per customer
- **AvgQuantity**: Average quantity per transaction
- **ProductCount**: Number of unique products purchased

## Customer Segmentation with K-Means
- Scaled features using `StandardScaler`
- Determined optimal `k` using:
  - Elbow Method (Within-Cluster Sum of Squares)
  - Davies-Bouldin Index (cluster separation)
- Selected `k=5` clusters for final segmentation
- Applied K-Means clustering and assigned each customer to a segment

## Cluster Analysis
Cluster-level summary statistics (unscaled values):
- **Dormant / At-Risk**: High recency, low spend → likely churned
- **Loyalist**: High frequency and monetary value → core repeat buyers
- **VIP / Elite**: Small group of extremely high-value customers
- **One-Off Bulk Buyers**: Rare but high-quantity purchases
- **Occasional Shoppers**: Largest segment, low frequency, moderate spend

## Marketing Strategies Based on Customer Segmentation
The identified segments provide clear opportunities for targeted marketing to improve retention, re-engagement, and overall customer lifetime value.

- **Loyalists** (high frequency & spend)
  - Maintain loyalty with exclusive perks, early access, and VIP treatment
  - Encourage advocacy through referral rewards and feedback loops
- **Dormant / At-Risk** (long recency, low spend)
  - Deploy win-back campaigns with discounts or limited-time offers
  - Showcase new products or send personalized reactivation messages
- **VIP / Elite** (very high monetary value, small group)
  - Provide personalized recommendations and priority service
  - Offer exclusive events or concierge-level support to strengthen relationships
- **One-Off Bulk Buyers** (rare, high-quantity purchases)
  - Target with bulk purchase discounts or B2B-oriented promotions
  - Send reminders when similar products are restocked
- **Occasional Shoppers** (largest segment, moderate activity)
  - Nurture with educational content, curated product suggestions, and small incentives
  - Encourage repeat purchases with “next order” discounts or loyalty point boosts

**Takeaway**: Tailoring campaigns to each group increases ROI by focusing spend where it drives the most impact — retaining high-value customers while reactivating or upselling lower-engagement segments.

## Segmentation Visualizations
- **Interactive Dashboard**: Customer counts and boxplots of behavioral features by cluster
- **3D PCA Plot**: Visual representation of clusters in reduced dimensional space

## Key Results
- Identified five distinct customer groups with meaningful business implications
- Provided actionable insights for targeted marketing (e.g., retention strategies for At-Risk, loyalty programs for VIPs, reactivation campaigns for Occasional Shoppers)
- Demonstrated how unsupervised learning can drive data-informed customer strategy

## Acknowledgments
- **Dataset**: UCI Machine Learning Repository – Online Retail Dataset

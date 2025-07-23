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

## Marketing Strategies Based on Customer Segmentation

Understanding the characteristics of each customer segment allows for the development of targeted marketing strategies that optimize spend and improve engagement. Based on the RFM and K-Means analysis, we can propose strategies focused on your key objectives: retaining loyal customers, re-engaging waning members, and engaging new members.

---

## 1. Retaining Loyal Customers (Champions / Loyalists)

**Characteristics**: These customers have high Recency, Frequency, and Monetary values. They are your most valuable customers and contribute significantly to revenue.

**Objective**: Maintain their loyalty, encourage continued high-value purchases, and potentially turn them into advocates.

**Potential Strategies**:

- **Exclusive Loyalty Programs**: Offer tiered loyalty programs with increasing benefits (discounts, early access to new products, free shipping) for higher levels of engagement and spending.
- **VIP Treatment**: Provide personalized communication, dedicated customer support, and invitations to exclusive events or sales.
- **Early Access and Sneak Peeks**: Give loyal customers a first look at new arrivals or upcoming promotions.
- **Personalized Recommendations**: Use their purchase history to recommend relevant products or categories.
- **Rewards for Referrals**: Encourage them to refer friends and family with attractive incentives for both the referrer and the new customer.
- **Gather Feedback**: Actively solicit feedback from loyal customers to understand their needs and improve the customer experience. This also makes them feel valued.
- **Surprise and Delight**: Occasionally send small gifts, personalized notes, or unexpected discounts to show appreciation.

---

## 2. Re-engaging Waning Members (Waning / At-Risk)

**Characteristics**: These customers show a decrease in Recency, Frequency, or Monetary values. They were once active but are now showing signs of reduced engagement.

**Objective**: Encourage them to make another purchase and bring them back into a more active state.

**Potential Strategies**:

- **Win-Back Campaigns**: Send targeted email or advertising campaigns with compelling offers (discounts, special promotions, freebies) to incentivize a return purchase.
- **Highlight New Products/Features**: Showcase new inventory or recently added features that might pique their interest based on their past purchases.
- **Reminders of Benefits**: Remind them of the value they received as a customer and the benefits of shopping with you.
- **Personalized Outreach**: If possible, a more personal touch through email or even a phone call (for high-value waning customers) to understand why they haven't been purchasing.
- **Surveys for Feedback**: Send short surveys to understand why their purchase behavior has changed and gather insights for improvement.
- **Limited-Time Offers**: Create a sense of urgency with time-sensitive discounts or promotions.

---

## 3. Engaging New Members (New Customers / Some 'Lost' with Recent Activity)

**Characteristics**: These customers have recently made their first purchase but have low frequency and monetary values so far.

**Objective**: Encourage repeat purchases, increase their engagement, and move them towards becoming loyal customers.

**Potential Strategies**:

- **Welcome Series**: Implement a series of welcome emails that introduce them to your brand, highlight key products or categories, and offer a small incentive for their second purchase.
- **Educational Content**: Provide helpful tips, tutorials, or guides related to the products they purchased to enhance their experience and encourage further exploration.
- **Showcase Popular Products**: Recommend best-selling or highly-rated products that other customers love.
- **Encourage Account Creation/Profile Completion**: Incentivize them to create an account or complete their profile to gather more information for future personalization.
- **Offer a "Next Purchase" Discount**: Provide a discount or special offer specifically for their second order.
- **Introduce Your Community**: If applicable, invite them to join your social media community or online forums to build a connection with your brand.

---

By tailoring your marketing efforts to the specific needs and behaviors of these identified customer segments, you can increase the effectiveness of your campaigns, improve customer satisfaction, and ultimately drive business growth.

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

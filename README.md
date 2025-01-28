# Zeotap_Data_Science



**1. Data Loading and Preparation:**

- **Import Libraries:**  Imports necessary libraries like NumPy, Pandas, scikit-learn (for clustering and metrics), and Google Colab's drive mounting functionality.
- **Mount Google Drive:** Mounts your Google Drive to access data files stored there.  This is specific to Google Colab.
- **Load Data:** Reads three CSV files (Customers, Products, Transactions) from your Google Drive into Pandas DataFrames.
- **Data Merging:** Merges the `Transactions` and `Customers` dataframes using the `CustomerID` column as a key.  A left merge ensures all transactions are kept, and customer information is joined where available.  The Products data is commented out, suggesting an initial attempt to incorporate it, but it's currently excluded from the clustering.
- **Data Aggregation:** Groups the merged data by `CustomerID` and calculates aggregate values:
    - `TotalValue`: Sum of total values for each customer.
    - `Quantity`: Sum of quantities purchased by each customer.
    - `Price`: Mean price of items purchased by each customer.
    - `Region`: The first encountered region for each customer (this could be improved if multiple regions per customer need to be handled).
- **One-Hot Encoding:** Converts the categorical 'Region' feature into numerical representations using one-hot encoding (`pd.get_dummies`).  This is crucial for K-Means, which works with numerical data.
- **Data Scaling:** Standardizes the features using `StandardScaler`.  This ensures that features with larger values don't dominate the clustering process.  It transforms the data to have zero mean and unit variance.

**2. Finding the Optimal Number of Clusters:**

- **Davies-Bouldin Index:** Uses the Davies-Bouldin index to determine the optimal number of clusters. The Davies-Bouldin index measures the average similarity between each cluster and its most similar cluster.  Lower values indicate better-defined clusters.
- **Iteration:** It iterates through a range of cluster counts (2 to 10) and calculates the Davies-Bouldin index for each.
- **Plotting:** Plots the Davies-Bouldin index values against the number of clusters.  This visualization helps identify the "elbow point," where the index starts to decrease more slowly, suggesting an optimal number of clusters.
- **Optimal K:** Determines the optimal k (number of clusters) based on the minimum Davies-Bouldin index value.


**3. K-Means Clustering and Evaluation:**

- **K-Means Clustering:** Performs K-Means clustering using the optimal `k` determined in the previous step. The `random_state` ensures reproducibility of the results.
- **Cluster Assignment:** Assigns cluster labels to each customer in the `customer_profile` DataFrame.
- **Visualization:** Creates a scatter plot to visualize the clusters based on total value and quantity.  This provides an intuitive understanding of how the customers are grouped.
- **Clustering Metrics:**
    - Prints the optimal number of clusters, Davies-Bouldin index, silhouette score, and Calinski-Harabasz index. These are used to assess the quality of the clustering.
    - **Silhouette Score:** Measures how similar a data point is to its own cluster compared to other clusters. Higher values are better.
    - **Calinski-Harabasz Index:**  Higher values indicate better-defined clusters. It measures the ratio of between-cluster variance to within-cluster variance.
- **Cluster Size Distribution:** Generates a bar chart showing the distribution of customers across the different clusters.

**4. Reporting:**

- Provides a summary of the clustering results including the optimal k and the quality metrics.


**Potential Improvements:**

- **Product Data Integration:** The code has commented-out lines for merging `Products` data.  Investigate why it was commented and explore whether including product information could improve segmentation.
- **Feature Engineering:** Explore additional features that could improve segmentation.  For example, frequency of purchases, average order value, product categories purchased, etc.
- **Other Clustering Algorithms:** Compare the results of K-Means with other clustering algorithms like DBSCAN or hierarchical clustering.  Different algorithms may perform better depending on the data distribution.
- **Region Handling:** If a customer might belong to multiple regions, explore better methods than taking the 'first' region.
- **More Robust Evaluation Metrics:** Explore other metrics like Dunn index and consider using a combination of metrics for a comprehensive evaluation.


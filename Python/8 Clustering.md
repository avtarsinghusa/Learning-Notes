# Clustering 
### Manhattan distance
* This is a **way to measure the distance between two points in clustering algorithms**.
* It is commonly used in machine learning methods like K-means clustering and K-nearest neighbors.
* Manhattan distance **calculates the sum of the absolute differences between coordinates of two points**.

        📊 Example
        Point A = (2, 3)
        Point B = (5, 7)
        
          Manhattan Distance: ∣2−5∣+∣3−7∣ =3+4=7
        So the distance between the two points is 7.
* In clustering algorithms, **Manhattan distance helps to**:
  * Measure similarity between data points
  * Assign points to the nearest cluster
  * Handle high-dimensional data better than Euclidean distance in some cases

### Euclidean Distance** (Straight-line distance) 
* This is the **shortest straight-line distance between two points** (like using a ruler).
      Visual intuition
      Imagine two points on a map:

          A •
             \
              \
               • B
      You go directly from A to B diagonally.

### Z-score scaling (also called standardization) 
* This is a data preprocessing technique used in machine learning to **normalize numerical features so they have a mean of 0 and a standard deviation of 1**.
* It is commonly used before algorithms like **K-means clustering**, **K-nearest neighbors**, and **Support Vector Machine** because these algorithms are sensitive to feature scale.
  * 📊 What it does - After applying Z-score scaling:
    * Mean of the feature → **0**
    * Standard deviation → **1**

* This ensures all features are **on the same scale**.
        z = (x - u)/σ
        Where:
        x = original value
        μ = mean of the feature
        σ = standard deviation
        z = standardized value (z-score)
        Example:
        
        | Original Values | Z-Score |
        | --------------- | ------- |
        | 50              | -1      |
        | 60              | 0       |
        | 70              | +1      |
        
        So:
        * Negative z-score → below average
        * Positive z-score → above average

  * **Why it is important in ML**

        Suppose a dataset has:
        | Feature | Range            |
        | ------- | ---------------- |
        | Age     | 18 – 60          |
        | Salary  | 30,000 – 200,000 |
        
        If you don't scale:
        * Salary dominates distance calculations
        * Clustering or KNN becomes biased.
        
        Z-score scaling fixes this by **making all features comparable**.

* **Z-score vs Min-Max scaling**

        | Feature      | Z-Score Scaling          | Min-Max Scaling       |
        | ------------ | ------------------------ | --------------------- |
        | Range        | No fixed range           | 0 to 1                |
        | Outliers     | Handles better           | Sensitive to outliers |
        | Distribution | Keeps distribution shape | Compresses values     |

* **Simple idea:** Z-score scaling tells **how far a value is from the mean in terms of standard deviations**.

### Connectivity-based clustering (Hierarchical clustering)
* This is a type of clustering method **where data points are grouped based on how close or connected they are to each other**. The idea is that points that are nearby form clusters, and clusters grow by connecting neighboring points.
#### 1️⃣ Basic idea
* Connectivity-based clustering assumes:
  * If point A is close to B, and B is close to C, then A, B, and C belong to the same cluster.
  * Clusters are formed by linking nearby points step-by-step.

#### 2️⃣ Hierarchical clustering
* **The most common connectivity-based clustering method is Hierarchical clustering.**
* **It builds clusters in a tree structure called a dendrogram.**
* Two main types:
  * Agglomerative (Bottom-Up)
    * Start with each point as its own cluster
    * Merge the closest clusters step by step
    * Continue until all points form one cluster

                Example:
                A   B   C   D
                ↓
                (A,B)   (C,D)
                ↓
                (A,B,C,D)

  * Divisive (Top-Down)
    * Start with all points in one cluster
    * Split them into smaller clusters step by step.

#### 3️⃣ How distance is measured
* Connectivity clustering uses distance metrics like: Euclidean distance / Manhattan distance / Cosine distance
* These help determine which points should connect first.

#### 4️⃣ Linkage methods
* When merging clusters, different linkage rules are used.

                Linkage	                Meaning
                Single linkage	distance between closest points
                Complete linkage	distance between farthest points
                Average linkage	average distance between clusters

*These affect the shape of clusters.

#### 5️⃣ Advantages

✔ No need to specify number of clusters initially

✔ Works well for small datasets

✔ Produces a dendrogram that shows cluster relationships

#### 6️⃣ Disadvantages

❌ Computationally expensive for large datasets

❌ Sensitive to noise and outliers

### 1️⃣ Centroid-based clustering
* The most common example is **K-means clustering**.

#### Idea
* Each cluster has a **center point (centroid)**.
* Data points are assigned to the **nearest centroid**.
* The centroid keeps updating until clusters stabilize.

#### Steps
1. Choose **K (number of clusters)**
2. Initialize **K centroids**
3. Assign each point to the nearest centroid
4. Recalculate centroids
5. Repeat until convergence

#### Pros
✔ Simple and fast

✔ Works well for large datasets

#### Cons

❌ Must choose **K beforehand**

❌ Sensitive to outliers

❌ Works best with **spherical clusters**

### 2️⃣ Density-based clustering
* A popular algorithm is **DBSCAN**.

#### Idea

Clusters are formed in **dense regions of data points** separated by sparse regions.

#### How it works

Points are classified as:

* **Core points** – many neighbors nearby
* **Border points** – near a cluster but not dense
* **Noise points** – outliers

#### Pros

✔ Detects **arbitrarily shaped clusters**

✔ Automatically detects **outliers**

#### Cons

❌ Hard to choose parameters (`eps`, `minPts`)

❌ Struggles when clusters have **different densities**

### 3️⃣ Distribution-based clustering
* A common method is **Gaussian Mixture Model (GMM)**.

#### Idea
* Data is assumed to come from **multiple probability distributions** (usually Gaussian).
* Each cluster is represented by a **probability distribution** rather than a hard boundary.

#### Key feature
* Points belong to clusters **with probabilities** instead of strictly belonging to one cluster.

        Example:
        * Point A → 70% Cluster 1
        * Point A → 30% Cluster 2

#### Pros

✔ Flexible cluster shapes

✔ Probabilistic clustering

#### Cons

❌ Computationally expensive

❌ Requires assumptions about distributions

#### 🧠 Quick comparison

        | Type               | Example Algorithm       | Key Idea                                      |
        | ------------------ | ----------------------- | --------------------------------------------- |
        | Connectivity-based | Hierarchical clustering | Connect nearby points                         |
        | Centroid-based     | K-means                 | Cluster around centroids                      |
        | Density-based      | DBSCAN                  | Dense regions form clusters                   |
        | Distribution-based | Gaussian Mixture Model  | Data generated from probability distributions |

### What is the Elbow Method?
* The Elbow Method is used in **K-means clustering to find the optimal number of clusters** (K).

#### Core idea
* As you increase the number of clusters:
  * The clustering error (distance within clusters) decreases
  * But after a point, improvement becomes very small
  * That “bend” point looks like an elbow → best K

#### 📉 What do we plot?
* We plot:
  * X-axis → Number of clusters (K)
  * Y-axis → Within-cluster sum of squares (WCSS)


#### How it works step-by-step
* Run K-means for different K values (e.g., 1 to 10)
* Compute WCSS for each K
* Plot the graph (K vs WCSS)
* Look for the “elbow point”
* That K is your optimal number of clusters

#### Intuition
* K = 1 → very high error
* Increasing K → error drops quickly
* After some K → error drops slowly
* The “knee” or “elbow” = best trade-off

#### Limitations
* Sometimes the elbow is not clear
* Subjective (depends on visual judgment)
* Doesn’t always work for complex data

### Silhouette Score (in clustering)
* The Silhouette Score is a better (and more quantitative) way than the elbow method to evaluate clustering quality in K-means clustering and similar algorithms.

#### Intuition
* It measures how well each data point fits into its cluster:
  * Close to its own cluster
  * Far from other clusters

#### Formula
* a(i): Average distance of point i to all other points in the same cluster
* b(i): Minimum average distance of point i to points in the nearest different cluster

           s(i) = (b(i) - a(i))/ max{a(i), b(i)}
           📈 Score Range
          Value  	        Meaning
          +1	        Perfect clustering (well separated)
           0	        Clusters overlap
          -1	        Wrong clustering (misclassified)
#### How to use it
* Run K-means for different values of K
* Compute silhouette score for each K
* Choose K with the highest score
* 👉 Unlike elbow, this gives a clear numeric answer
* If a point is:
  * Very close to its cluster → a small
  * Far from others → b large
  * 👉 Score ≈ 1 (good)
* If clusters overlap:
  * 👉 Score ≈ 0
* Wrong clustering (misclassified)
  * * 👉 Score ≈ -1

                ⚖️ Silhouette vs Elbow Method
                Feature	        Elbow Method	Silhouette Score
                Type	        Visual        	Numeric
                Output	        Graph	        Score
                Accuracy	Medium	        Higher
                Ease	        Very simple	Slightly more computation
### 📊 Cluster Profiling (in clustering)
* Cluster profiling is the process of understanding and describing each cluster after applying algorithms like K-means clustering.
* 👉 In simple terms:
  *After grouping data, you ask: “What does each group represent?”

#### Why it’s important
* Clustering alone just gives labels (Cluster 1, 2, 3…).
* Profiling helps you:
  * Interpret clusters meaningfully
  * Make business or research decisions
  * Identify patterns and differences between groups

#### 🔍 How cluster profiling is done
##### 1. Statistical summary
* For each cluster, compute:
  * Mean / median of features
  * Standard deviation
  * Min–max values
                👉 Example:
                Cluster 1 → young users, low income
                Cluster 2 → older users, high income
##### 2. Compare across clusters
* Look at how features differ:
  * Which feature is high or low in each cluster
  * What makes a cluster unique
##### 3. Use visualizations
* Bar charts
* Box plots
* Heatmaps
* 👉 Helps quickly see differences between clusters

##### 4. Assign labels (very important)
* Give meaningful names like:
  * “High-value customers”
  * “Budget buyers”
  * “Frequent users”

                📊 Example
                Suppose you clustered customers:
                
                Cluster	Age	Income	Spending
                1	Low	Low	Low
                2	Medium	Medium	Medium
                3	High	High	High

                👉 Profiles:
                Cluster 1 → “Low-income group”
                Cluster 3 → “Premium customers”
#### ✅ Final takeaway
* Clustering = grouping data
* Cluster profiling = understanding those groups
* **It turns raw clusters into actionable insights**

### Dimensionality Reduction
* **Dimensionality reduction** is the process of **reducing the number of features (variables)** in a dataset while keeping as much important information as possible.
#### 🧠 Why it is needed
* High-dimensional data can cause problems like:
  * Overfitting
  * Slow computation
  * Hard visualization
  * Curse of dimensionality (**Curse of Dimensionality**)
  * 👉 So we reduce dimensions to make models simpler and more efficient.


#### 🔍 Types of Dimensionality Reduction
##### 1. Feature Selection
* Select a subset of original features
  * Remove irrelevant or redundant features
  * Example: keep only important columns
##### 2. Feature Extraction
* Create new features from old ones
  * Combines existing variables
  * Example:
     * **Principal Component Analysis (PCA)** (most popular)
     * * **Linear Discriminant Analysis**

                Example (PCA idea)
                * Original: 100 features
                * After PCA: 2–3 components
                  👉 Still captures most variance in data
* **Feature Extraction Common Techniques** 
  * **Principal Component Analysis** → variance-based
    * **Principal Component Analysis (PCA)** is a statistical and machine-learning technique for dimensionality reduction. It transforms correlated variables into a smaller set of uncorrelated variables called principal components that capture most of the data’s variance. PCA is widely used for preprocessing, visualization, and noise reduction in high-dimensional datasets. 
  * **t-SNE** → visualization
  * **UMAP** → faster, preserves structure
  * **Autoencoders** → deep learning approach

####  Benefits of Dimensionality Reduction
* Faster training
* Less storage
* Removes noise
* Better visualization (2D/3D plots)

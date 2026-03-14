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

The most common connectivity-based clustering method is
Hierarchical clustering.

It builds clusters in a tree structure called a dendrogram.

Two main types:

Agglomerative (Bottom-Up)

Start with each point as its own cluster

Merge the closest clusters step by step

Continue until all points form one cluster

Example:

A   B   C   D
↓
(A,B)   (C,D)
↓
(A,B,C,D)
Divisive (Top-Down)

Start with all points in one cluster

Split them into smaller clusters step by step.

3️⃣ How distance is measured

Connectivity clustering uses distance metrics like:

Euclidean distance

Manhattan distance

Cosine distance

These help determine which points should connect first.

4️⃣ Linkage methods

When merging clusters, different linkage rules are used.

Linkage	Meaning
Single linkage	distance between closest points
Complete linkage	distance between farthest points
Average linkage	average distance between clusters

These affect the shape of clusters.

5️⃣ Example intuition

Imagine people standing in a field.

If two people are close, they join a group.
Then nearby groups merge together.

Eventually clusters form based on distance connectivity.

6️⃣ Advantages

✔ No need to specify number of clusters initially
✔ Works well for small datasets
✔ Produces a dendrogram that shows cluster relationships

7️⃣ Disadvantages

❌ Computationally expensive for large datasets
❌ Sensitive to noise and outliers

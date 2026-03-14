# Decision Tree
* A Decision Tree is a supervised machine learning algorithm used for classification and regression.
* It works by splitting the data into branches based on feature values, forming a structure similar to a tree.
* The model makes decisions by asking a sequence of if–else questions about the features.
### Types of Decision Trees
#### 1️⃣ Classification Tree
* Used when the target variable is categorical.
  * Example: Spam or Not Spam ,  Buy or Not Buy, Disease: Yes / No

#### 2️⃣ Regression Tree
* Used when the target variable is continuous.
  * Example: House price prediction, Sales prediction

#### How Decision Trees Choose Splits
* The algorithm selects the best feature using measures such as:
  * Gini Index
  * Entropy / Information Gain
  * Variance Reduction (for regression)

### Impurity Measures in Decision Trees
* Impurity measures are fundamental concepts in decision tree algorithms that quantify how "mixed" or "pure" a set of data is at each node. They help determine which features to split on and when to stop growing the tree.

#### **What is Impurity?**
* Impurity reflects the degree of disorder or heterogeneity in a dataset. A node with impurity of zero means all samples belong to a single class (pure node), while high impurity indicates samples from multiple classes are mixed together (impure node). The goal of decision trees is to recursively split data to minimize impurity and create homogeneous groups.

### **Main Impurity Measures**
**Gini Impurity** is widely used in classification tree algorithms like CART (Classification and Regression Trees). 

**Entropy** is another common measure, particularly used in ID3 and C4.5 algorithms. 

### How They're Used in Tree Building
* During tree construction, the algorithm evaluates all possible splits for each feature at each node. For each potential split, it calculates the impurity of the resulting child nodes and measures the reduction in impurity compared to the parent node. The split that provides the maximum impurity reduction (or information gain) is selected. **This greedy approach continues until stopping criteria are met, such as reaching maximum depth, minimum samples per node, or achieving zero impurity.**
* **If a node has three classes with probabilities 0.2, 0.5, and 0.3, what is the Gini impurity?**
  * Step-by-Step Calculation
  * Identify the probabilities (p):
  * p1​=0.2, p2​=0.5, p3​=0.3
  * Square each probability:
  *  (0.2)2=0.04, (0.5)2=0.25, (0.3)2=0.09
  *  Sum the squared probabilities: 0.04+0.25+0.09=0.38
  *  Subtract the sum from 1: 1−0.38=0.62
  *  Result : The Gini impurity for the node is 0.62.
 
### Decision Tree Evaluation Metrics: Types and When to Use Them
* Decision tree evaluation metrics are used to assess how well a trained model performs on classification or regression tasks. Choosing the right metrics depends on your problem type, data characteristics, and business objectives.
#### Classification Metrics
* **Accuracy** measures the proportion of correct predictions among all predictions:

  Accuracy= (True Positives + True Negatives) / Total Samples​
  * **Use accuracy when you have balanced datasets** where all classes are equally important and misclassification costs are uniform. However, avoid it for imbalanced datasets where one class dominates, as a model predicting the majority class could achieve high accuracy despite poor performance on minority classes.

* **Precision** focuses on the reliability of positive predictions:

  Precision= True Positives / (True Positives + False Positives)​

  * **Use precision when the cost of false positives is high**. Common applications include spam detection (you don't want legitimate emails marked as spam), medical diagnoses where false alarms create unnecessary patient anxiety, or fraud detection systems where false positives waste investigation resources.

* **Recall** (also called **Sensitivity**) measures the model's ability to identify all positive cases:

  Recall= True Positives​ / (True Positives + False Negatives)

  * **Use recall when the cost of false negatives is high and missing positive cases is problematic.** This applies to disease screening (missing a patient with cancer could be life-threatening), security threat detection (missing an intrusion attempt is critical), or defect detection in manufacturing (allowing defective products to reach customers is costly).

* **F1-Score** is the harmonic mean of precision and recall:

  F1-Score=2× (Precision × Recall) / (Precision + Recall)​

   * **Use F1-Score when you need a single metric that balances both false positives and false negatives**, particularly useful for imbalanced datasets. It's valuable when precision and recall are equally important, like in information retrieval systems or multi-class classification problems.
 
### Cost Complexity Pruning (CCP) in Decision Trees 🌳✂️
* Cost Complexity Pruning is a post-pruning method used to simplify a decision tree by removing branches that do not significantly improve prediction accuracy.
* It is mainly used in the CART (Classification and Regression Tree) algorithm.
* The idea is to balance two things:
 * Model accuracy
 * Tree complexity (number of nodes/leaves)
 The Cost Complexity Formula
 Rα(T)=R(T)+α∣T∣

  Where:
  * R(T) → Error of the decision tree on training data
  * |T| → Number of leaf nodes in the tree
  * α (alpha) → Complexity parameter (penalty for large trees)
 
 Meaning
 * If the tree becomes too complex, the penalty term α|T| increases.
 * The algorithm removes branches that increase complexity without improving accuracy.

α (alpha) = (Error(Pruned) - Error(Original)) / Number of nodes reduced

**Smaller α (alpha) means** - Smaller drop in the performance per node lost.

**Optimal α (alpha) value correspond to the tree having the lowest error on unseen(test) data.**

**How Cost Complexity Pruning Works**
 * Step 1: Build a full decision tree (very deep tree).
 * Step 2: Calculate the cost complexity for each subtree.
 * Step 3: Remove branches that increase the cost function.
 * Step 4: Select the optimal subtree based on the best α value.

Example
Original Tree (Complex)

Age > 30

 ├── Income > 50k
 
   │ ├── City A → Buy
 
   │ └── City B → Buy
 
 └── Income <= 50k → Don't Buy

Here both City A and City B lead to Buy, so splitting by city adds complexity but no benefit.

After Pruning

Age > 30

 ├── Income > 50k → Buy
 
 └── Income <= 50k → Don't Buy

The unnecessary branch is removed.

**Role of α (Alpha)**

Alpha Value   	Effect

**α = 0**         	No pruning (full tree)

**Small α**	        Slight pruning

**Large α**	         Strong pruning (smaller tree)

**So α controls how aggressively the tree is pruned.**

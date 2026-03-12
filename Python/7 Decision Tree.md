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

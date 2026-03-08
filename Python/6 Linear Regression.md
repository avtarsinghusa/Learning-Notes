# Linear Regression
### Machine Learning tasks
#### 1.Supervised learning:
  * Building a mathematical model using **data that contains both the inputs and the desired outputs** (ground truth). 
    * Examples: 
      * Determining if an image has a horse. The data would include images with and without the horse (the input), 
      and for each image we would have a label (the output) indicating if there is a horse in that image. 
      * Determining is a client might default on a loan
      * Determining if a call center employee is likely to quit
    * **Since we have desired outputs, model performance can be evaluated by comparisons.**
#### 2.Unsupervised learning:
* Building a mathematical model using data that contains only inputs and no desired outputs.
* **Used to find structure in the data, like grouping or clustering of data points**. To discover patterns and group the inputs into categories.
* Example:
  * An advertising platform segments the population into smaller groups with similar demographics and purchasing habits. Helping advertisers reach their target market with relevant ads.
  * Since no labels are provided, there is no specific way to compare model performance in most unsupervised learning methods.
### Tools and techniques
#### Supervised learning
  * **Regression**: desired output is a continuous number.
  * **Classification**: desired output is a category.
#### Unsupervised learning
  * **Clustering**: Grouping data.
  * **Dimensionality reduction**: Compressing data.
  * **Association rule learning**: If X then Y
### Linear regression -- 
* Linear regression models the relationship as a straight line, and multiple regression, which involves more than one independent variable. This technique is widely used for prediction, forecasting, and identifying causal relationships.
* The **vertical distances** are a measure of how far away the prediction is from the actual value, and **these are called residuals**. We **aim to reduce** the sum of the magnitudes of these residuals which helps the predicted values to get closer to the actual values. The objective of linear regression is to minimize the sum of squared vertical distances.

#### When developing a regression model, you work with two main types of variables:
##### 1. Independent Variables (Predictor / Input Variables)
These are the variables **you use to predict or explain something**.
They are the **inputs** to the model.
* Represented as **X**
* They **influence or help explain** another variable
* You can have **one or many** independent variables

**Examples**
 * House price prediction
   * Size of house (X₁)
   * Number of bedrooms (X₂)
   * Location score (X₃)
 * Student performance prediction
   * Hours studied (X₁)
   * Attendance (X₂)

##### 2. Dependent Variable (Target / Response Variable)
This is the variable **you want to predict or explain**.
* Represented as **Y**
* Its value **depends on the independent variables**

**Examples**
* House price (**Y**)
* Student exam score (**Y**)
* Sales revenue (**Y**)

**Example Regression Model:**

**Simple Linear Regression:** 
**Y=β0​+β1​X+ϵ**
* **Y** → Dependent variable (what we predict)
* **X** → Independent variable (predictor)
* **β₀** → Intercept (The average value of response when the explanatory variable is 0)
* **β₁** → Coefficient (effect of X on Y) (The average change in the response for one unit increase in the explanatory variable)
* **ε** → Error term

**Multiple Regression Example:**

**Y=β0​+β1​X1​+β2​X2​+β3​X3​+ϵ**

Example:
* **Y** = House Price
* **X₁** = Size of house
* **X₂** = Number of bedrooms
* **X₃** = Distance from city center

✅ **Summary**

| Variable Type        | Meaning                | Symbol |
| -------------------- | ---------------------- | ------ |
| Independent Variable | Input used to predict  | X      |
| Dependent Variable   | Output being predicted | Y      |

* **Correlation** is a **statistical measure** that describes **the extent to which two variables are related to each other** OR that describes **the strength and direction** of a **relationship** between two variables. It typcially **ranges between -1 and 1**.
*A **linear relationship** between two variables is one in which the **rate of change between the two is constant**. Example: The relationship between the distance traveled and the time taken at a constant speed.

### Pearson’s Correlation Coefficient:
* A statistical measure that quantifies the **strength and direction of the linear relationship between two continuous variables**. One of the most commonly used measures of correlation.

**Causation** means that one variable directly causes a change in another variable.
  In other words, when one event (the cause) happens, it produces an effect in another variable.

Example

Studying more hours → Higher exam scores

Studying more causes the improvement in scores.

Smoking → Increased risk of lung disease

Smoking causes damage that leads to disease.

**Causation vs Correlation**

Correlation: Two variables are related or move together.

Causation: One variable directly affects the other.

Example:

Ice cream sales and drowning incidents may both increase in summer (correlation), but ice cream sales do not cause drowning.

✅ Simple definition: Causation is when one variable directly produces a change in another variable (cause and effect).

### Categorical variables:
* Categorical variables are variables that represent groups or categories rather than numerical values. They are mainly divided into two types:


**1. Nominal Variables**

Nominal variables are categories **without any natural order or ranking**.

Examples

Gender: Male, Female

Blood group: A, B, AB, O

Colors: Red, Blue, Green

Country names

Key feature:
**There is no meaningful order between the categories.**

Example:
Red is not greater or smaller than Blue.

**2. Ordinal Variables**

Ordinal variables are categories that **have a meaningful order or ranking**, but the difference between categories is not precisely measurable.

Examples

Education level: High School → Bachelor’s → Master’s → PhD

Satisfaction level: Poor → Fair → Good → Excellent

Movie ratings: 1 star → 2 stars → 3 stars → 4 stars → 5 stars

Key feature:
The categories follow a logical order, but the distance between them is not necessarily equal.

Example:
The difference between Good and Excellent may not be the same as between Fair and Good.

### Encoding the Categorical Variables
* When using categorical variables in regression or machine learning, they must be converted into numbers. This process is called encoding. The main types of encoding are:

**1. Label Encoding**
Each category is assigned a unique number.

Example

Color	Encoded Value

Red	0
Blue	1
Green	2

Use case:
**Often used for ordinal variables where categories have an order.**

Example:
Low = 1, Medium = 2, High = 3

**2. One-Hot Encoding (Dummy Encoding)**

Each category becomes a separate binary column (0 or 1).

Example

Color	Red	Blue	Green

Red	   1	  0	   0

Blue	  0	  1   	0

Green 	0	  0	   1

Use case:
**Best for nominal variables where categories have no order.**

**MAE (Mean Absolute Error)** is a metric used to **measure the accuracy of a regression model**. It calculates the average absolute difference between the actual values and the predicted values. 📊

Definition

MAE tells us how far the model’s predictions are from the real values on average.

Example

Actual Value	Predicted Value	Absolute Error

100	90	10

150	140	10

200	210	10

MAE=(10+10+10)/3=10

So the model’s predictions are off by 10 units on average.

### Model Performance Evaluation
* **RMSE** (Root Mean Squared Error): RMSE measures the square root of the average squared differences between actual and predicted values, providing a metric that is in the same units as the target variable and penalizes larger errors more heavily.
* **MAPE** (Mean Absolute Percentage Error): MAPE calculates the average absolute percentage difference between actual and predicted values, expressing prediction accuracy as a percentage and allowing for easy interpretation across different scales.
* **R²** (Coefficient of Determination): R² indicates the proportion of the variance in the dependent variable that is predictable from the independent variables, with values closer to 1 signifying a better fit. **Note:** **R-squared individually can’t tell whether a variable is useful for prediction or not**. Whenever we add a new variable, the R-squared value will increase. But, that is not true in the case of **adjusted R-squared, which increases only when the added variable is useful for model prediction.**
* **MAE** (Mean Absolute Error): MAE measures the average absolute difference between the actual and predicted values, providing a straightforward metric of prediction accuracy.

**Simple Linear Regression - Sales vs Advertising Expenditure**

      RMSE 	        MAE 	         MAPE 	   R-squared 	Adj R-squared

      2753.419094 	2207.551603 	9.647262 	 0.415783 	  0.415539

* The performance metrics evaluate how well your linear regression model predicts **Sales based on Advertising Expenditure**.
Here is how to interpret each value to understand your model's "health":

**1. Error Metrics (The "How Far Off Are We?" Section)**

These values represent the distance between what your model predicted and what actually happened. **Lower is better.**

   **MAE** (Mean Absolute Error): 2207.55

  On average, your model’s sales predictions are off by about 2,208 units (or dollars, depending on your currency). This is a direct, easy-to-understand average of all errors.

   **RMSE** (Root Mean Square Error): 2753.42

  Like MAE, this measures error, but it "punishes" larger mistakes more severely. Since your RMSE is significantly higher than your MAE, it suggests you have some outliers—specific cases where the model was way off.

   **MAPE** (Mean Absolute Percentage Error): 9.65%

   **This is often the most useful for business stakeholders**. It tells you that, on average, **your predictions are within 90.35% accuracy (100% - 9.65%)**. 
   **A MAPE under 10% is generally considered an excellent prediction for sales data.**

**2. Goodness-of-Fit (The "How Much Do We Know?" Section)**

These values range from 0 to 1 and tell you how much of the "story" your variables are telling. Higher is better.

   **R-squared**: 0.4158

   This means **Advertising Expenditure explains about 41.6% of the variation in your Sales.**

   The **remaining 58.4% is caused by things not in this specific model** (like the Discounts we discussed earlier, seasonality, or competitor actions).

   **Adj R-squared:** 0.4155

    This is a "honest" version of R-squared. It adjusts the score based on how many variables you use. Since you only have one variable here, it is almost identical to the regular R-squared.

Summary Table for Quick Reference

    Metric	      Value	      Interpretation

    Accuracy	   ~90.35%	    Excellent for most business use cases.

    Typical Error	2,208	    The average "miss" per prediction.

    Explanatory Power	41.6%	Ads are a major factor, but more than half of your sales are driven by other things.

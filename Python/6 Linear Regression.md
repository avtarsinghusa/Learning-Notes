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

**Example Regression Model**
**Simple Linear Regression:** 
**Y=β0​+β1​X+ϵ**
* **Y** → Dependent variable (what we predict)
* **X** → Independent variable (predictor)
* **β₀** → Intercept
* **β₁** → Coefficient (effect of X on Y)
* **ε** → Error term

## Multiple Regression Example: 
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


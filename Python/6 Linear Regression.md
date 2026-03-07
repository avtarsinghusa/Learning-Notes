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

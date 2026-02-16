### Data Visualization -- Week 3
```
# Libraries to help with data visualization
import matplotlib.pyplot as plt
import seaborn as sns

# Command to tell Python to actually display the graphs
%matplotlib inline
```
#### Histogram
* **A histogram is a univariate plot which helps us understand the distribution of a continuous numerical variable.**
* It breaks the range of the continuous variables into a intervals of equal length and then counts the number of observations in each interval.
* We will use the **histplot() function** of seaborn to create histograms.
```
sns.histplot(data=df, x='price') # x='price' name of the column
```
**Let's see how we can customize a histogram.**
```plt.title('Histogram:Price')
plt.xlim(3000,50000)
plt.ylim(0,70)
plt.xlabel('Price of cars')
plt.ylabel('Frequency')
sns.histplot(data=df, x='price',color='orange');
```
* We can **specify the number of intervals** (or groups or bins) to create by setting the **bins parameter**.
* If not specified it is passed to numpy.histogram_bin_edges()
```
sns.histplot(data=df, x='price', bins=5)  # bins are the number of bars dipslayed.
```
* If we want to specify the **width of the intervals** (or groups or bins), we can use **binwidth parameter**.
```
sns.histplot(data=df, x='price', binwidth=20)
```
* **In addition to the bars, we can also add a density estimate by setting the *kde* parameter to *True*.**
 * **Kernel Density Estimation**, or **KDE**, visualizes the distribution of data over a continuous interval.
 * The conventional scale for KDE is: **Total frequency of each bin × Probability**
 * Note: if we increase the number of bins, it reduces the frequency count in each group (bin). Since the scale of KDE depends on the total frequency of each bin (group).
```
sns.histplot(data=df, x='price', kde=True);
```
* A histogram is said to be **symmetric** if the left-hand and right-hand sides resemble mirror images of each other when the histogram is cut down the middle.
* The tallest clusters of bars, i.e., peaks, in a histogram represent the **modes** of the data.
* A histogram **skewed to the right** has a large number of occurrences on the left side of the plot and a few on the right side of the plot. (**Skewed** -- suddenly change direction or position.)
* Similarly, a histogram **skewed to the left** has a large number of occurrences on the right side of the plot and few on the left side of the plot.

* **Histograms are intuitive but it is hardly a good choice when we want to compare the distributions of several groups**.
* For example, Show price for different body style (Convertible, hatchback, sedan, wagon, hardtop etc) in one graph the view will not be clear.
* **hue** -- parameter of the histplot() function can be used to create separate histograms for different categories groups and display them by stacking into one histogram
```
sns.histplot(data=df, x='price', hue='body_style', kde=True);
```
**It might be better to use subplots!** Now for each body_style, a separate graph is displyaed. 
```
g = sns.FacetGrid(df, col="body_style")
g.map(sns.histplot, "price");
```
#### Boxplot
* A **boxplot**, or a **box-and-whisker plot**, shows the distribution of **numerical data** and skewness through displaying the data quartiles
* It is also called a **five-number summary plot**, where the five-number summary includes the **minimum value, first quartile, median, third quartile, and the maximum value**.
* The **boxplot()** function of seaborn can be used to create a boxplot.
```
# creating a boxplot with seaborn
sns.boxplot(data=df, x='curb_weight');
```
**Let's see how we can customize a boxplot.**
```
plt.title('Boxplot:Horsepower')
plt.xlim(30,300)
plt.xlabel('Horsepower')
sns.axes_style('whitegrid')
sns.boxplot(data=df, x='horsepower',color='green');
```
* In a boxplot, when the median is closer to the left of the box and the whisker is shorter on the left end of the box,
  we say that the distribution is **positively skewed (skewed right)**.
* Similarly, when the median is closer to the right of the box and the whisker is shorter on the right end of the box,
  we say that the distribution is **negatively skewed (skewed left)**.
* **Outliers** are points that lie outside the minimum and maximum value of the boxplot. They are calculated by using the following equations:
  * For outliers on the left-hand side(towards the minimum side) of the data: **Q1-1.5*IQR**
  * For outliers on the right-hand side(towards the maximum side) of the data: **Q3+1.5*IQR**
 
**A boxplot (or box-and-whisker plot) is best used when** you want to **compare the distribution of a numerical variable across different categorical groups** or to quickly identify **outliers** in a dataset.
Here is when to use a boxplot specifically:
#### 1. Comparing Distributions Across Categories
If you have one numerical variable (e.g., `price`) and one categorical variable (e.g., `brand`), a boxplot allows you to see the spread, median, and skewness of prices for each brand side-by-side.
**Example:** Comparing the `salary` of employees across different `departments`.

#### 2. Identifying Outliers
Boxplots are excellent for spotting data points that fall far outside the general range of the data (the whiskers). These are represented as individual dots beyond the whiskers.

#### 3. Understanding Data Spread (Interquartile Range)
Unlike a histogram, which shows the shape of a distribution, a boxplot focuses on the **summary statistics**:

* **Median (line inside the box):** The central value.
* **IQR (the box):** The middle 50% of your data.
* **Whiskers:** The range of the remaining data (excluding outliers).

#### When to use a Histogram instead
Use a **histogram** when you want to see the shape of the data for a **single variable** (e.g., is it bimodal, skewed, or normally distributed?). Use a **boxplot** when you need to compare that shape across **multiple groups**.

#### Bar Graph
* A bar graph is generally used to **show the counts of observations in each bin** (or level or group) **of categorical variable** using bars.
* We can use the **countplot()** function of seaborn to plot a bar graph.
```
sns.countplot(data=df, x='body_style');
# We can also make the plot more granular by specifying the hue parameter to display counts for subgroups.
sns.countplot(data=df, x='body_style', hue='fuel_type');

# Let's increase the size of the plot to make it look better.
plt.figure(figsize=(20,7))
sns.countplot(data=df, x='make');

# Some of the tick marks on the x-axis are overlapping with each other.
# Let's rotate the tick marks to make it look better.
plt.figure(figsize=(20,7))
sns.countplot(data=df, x='make')
plt.xticks(rotation=90)

# A lot of plot-specific text has shown up in the output.
# Let's see how we can get rid of those.
plt.figure(figsize=(20,7))
sns.countplot(data=df, x='make')
plt.xticks(rotation=90)
plt.show() # this will ensure that the plot is displayed without the text
```
**Here are some common ways to customize a barplot.**
```
plt.figure(figsize=(10,7))
plt.title('Barplot:Engine-type')
plt.ylim(0,180) # Range on the y-axis
sns.countplot(data=df, x='engine_type',hue='fuel_type')
plt.xlabel('Engine-type');
```
#### Lineplot
Suppose, **your dataset has multiple y values for each x value**. **A lineplot is a great way to visualize this.** This type of data often shows up **when we have data that evolves over time**, for example, when we have monthly data over several years. If we want to compare the individual months, then a line plot is a great option. This is sometimes called **seasonality analysis.**
* A **line plot** uses straight lines to connect individual data points to display a trend or pattern in the data.
    - For example, seasonal effects and large changes over time.
* The **lineplot()** function of seaborn, by default, aggregates over multiple y values at each value of x and uses an estimate of the central tendency for the plot.
* **lineplot()** assumes that you are most often trying to draw y as a function of x. So, by default, it sorts the data by the x values before plotting.
```
# loading one of the example datasets available in seaborn
flights = sns.load_dataset("flights")

# creating a line plot
sns.lineplot(data = flights , x = 'month' , y = 'passengers');

# The light blue shaded area is actually the 'confidence interval' of the y-value estimates for each x-axis value.
# The confidence interval is a range of values around that estimate that are believed to contain the true value of that estimate with a certain probability.
# We can switch off the confidence intervals by setting the ci parameter to 'False'.
sns.lineplot(data = flights , x = 'month' , y = 'passengers', ci = False);
```
* We can also c**heck the relationship between two variables for different categories** by specifying the **hue** parameter.
```
sns.lineplot(data=flights,x = 'month' , y = 'passengers', ci = False ,hue='year');
```
* We can **change the style** of the lines by adding **style** parameter to the function.
```
# loading one of the example datasets available in seaborn
fmri = sns.load_dataset("fmri")

# creating the line plot
sns.lineplot(data = fmri, x="timepoint", y="signal", hue="region", style="region", ci = False);
```
* We can also **add markers** at each observation to identify groups in a better way.
```
sns.lineplot(data = fmri, x="timepoint", y="signal", hue="region", style="region", ci = False, markers = True);
```
**Let's customize the lineplot for a better visualization.**
```
plt.figure(figsize = (15,7))
sns.lineplot(data = flights , x = 'month' , y = 'passengers', hue = 'year')
plt.ylabel('Number of Passengers')
plt.legend(bbox_to_anchor=[1, 1]); #another way to change the legend's location in the plot
```
* **Note that**, unlike barplots and histograms, line plots may not include a zero baseline.
* We create a line chart is to emphasize changes in value, rather than the magnitude of the values themselves, and hence, a zero line is not meaningful.

#### Scatterplot
Sometimes we want to know **if two variables mean something when put together**, whether a small change in one variable affects the other variable. In such cases, plotting a **scatterplot**, or **scatter-diagram**, with our data points can help us to check whether there is a potential relationship between them.
* A scatterplot is the simplest mode of a diagrammatic representation of two variables.
* It takes two perpendicular axes of coordinates, one for x and one for y.
* Unlike the lineplot, it directly plots each pair of values as a point on the 2D space.
* The s**catterplot()** function of seaborn can be used to make a scatterplot.
```
sns.scatterplot(data=df, x='engine_size', y='horsepower');
```
* We can also check the relationship between two variables for different categories by specifying the **hue** parameter.
```
sns.scatterplot(data=df, x='engine_size', y='horsepower', hue='fuel_type');
```
* We can assign the **same variable as hue to another parameter style** which will vary the markers and create a more readable plot.
```
sns.scatterplot(data=df, x='engine_size', y='horsepower', hue='fuel_type', style='fuel_type');
```
* **Correlation** means association. More precisely, it expresses the extent to which two variables change together at a constant rate.
- In a scatter plot when the y variable tends to increase as the x variable increases, we say there is a **positive correlation** between the variables.
- Again, when the y variable tends to decrease as the x variable increases, we say there is a **negative correlation** between the variables.
- If the points on the scatter plot seem to be scattered randomly, we say that there is **no correlation** between the variables.
* **Note**: A **strong correlation** will have **data points close together**, while a **weak correlation** will have **data points that are further apart**.
* We can not measure the relationship quantitatively using a scatter plot. It just gives an expression for the relative change between the variables.

#### Pair Plot
* A pairplot **shows the relationship between two numeric variables for each pair of columns in the dataset**.
* It creates a grid of axes such that each variable in data will be shared in the y-axis across a single row and in the x-axis across a single column.
* The **pairplot()** function of seaborn can be used to create such a plot.
```
sns.pairplot(data=df[['normalized_losses','wheel_base','curb_weight','engine_size','price','peak_rpm']])

# We can add the hue parameter in pairplot to create a semantic mapping. It changes the default marginal plot to a layered kde plot.
sns.pairplot(data=df, vars=['wheel_base', 'curb_weight', 'engine_size', 'price'], hue='number_of_doors');

# We can set corner=True to plot only the lower triangle of a pairplot.
sns.pairplot(data=df, vars=['wheel_base', 'curb_weight', 'engine_size', 'price'], corner=True);
```

#### Heat Map
* A heatmap is a graphical representation of data as a color-encoded matrix.
* It is a great way of representing the correlation for each pair of columns in the data.
* The **heatmap()** function of seaborn helps us to create such a plot.
* In a heatmap, the **colors typically represent Frequency**.
* Heat mpas are commonly use in web analytics to visualize user interactions on websites.
```
sns.heatmap(data=df[['wheel_base','curb_weight','engine_size','price']].corr());

# We can set the annot parameter to True for displaying the numeric value in each cell.
# To remove the color bar, the cbar parameter can be set to False.
sns.heatmap(data=df[['wheel_base','curb_weight','engine_size','price']].corr(), annot=True, cbar=False);

# We can apply a different colormap with the cmap parameter for better visual appeal.
sns.heatmap(data=df[['wheel_base','curb_weight','engine_size','price']].corr(), annot=True, cmap='YlGnBu');
```

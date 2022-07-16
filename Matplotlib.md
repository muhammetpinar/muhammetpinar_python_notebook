# Matplotlib

## Basics of Matplotlib

First step you need to install and load matplotlib library. It must be already installed if you used Anaconda for setting up Python environment.

### Install library

If matplotlib is not already installed, you can install it by using the command

```
pip install matplotlib
```

### Import / Load Library

We will import Matplotlib’s Pyplot module and used alias or short-form as

```
plt
```

```
from matplotlib import pyplot as plt
```

### Elements of Graph

Different elements or parts of a standard graph are shown in the image below -

![https://3.bp.blogspot.com/-AtPG_12l4e8/XRSuQEECZGI/AAAAAAAAHxY/ZsgtA4rMphMZujcWUur9BB-xYKoWDkKPQCLcBGAs/s1600/basics_matplotlib.PNG](https://3.bp.blogspot.com/-AtPG_12l4e8/XRSuQEECZGI/AAAAAAAAHxY/ZsgtA4rMphMZujcWUur9BB-xYKoWDkKPQCLcBGAs/s1600/basics_matplotlib.PNG)

Figure

You can think of the figure as a big graph consisting of multiple sub-plots. Sub-plot can be one or more than one on a figure. In graphics world, it is called 'canvas'.

![https://2.bp.blogspot.com/-F__I5bCe3uI/XRS1Y3gdP9I/AAAAAAAAHxk/plElt8VRYRMp42BuHTe9wkD29hZaPvo-ACLcBGAs/s1600/figure_axes.PNG](https://2.bp.blogspot.com/-F__I5bCe3uI/XRS1Y3gdP9I/AAAAAAAAHxk/plElt8VRYRMp42BuHTe9wkD29hZaPvo-ACLcBGAs/s1600/figure_axes.PNG)

Axes

You can call them 'sub-plots'.

Axis

It's the same thing (x or y-axis) which you studied in school or college. A standard graph shows the marks on the axis. In matplotlib library, it is called

```
ticks
```

and text or value in ticks is called

```
ticklabels
```

.

Basic Plot

```
x = [1, 2, 3, 4, 5]
y = [5, 7, 3, 8, 4]
plt.bar(x,y)
plt.show()

```

![https://1.bp.blogspot.com/-bamSdPlBdas/XRD7aKeEgSI/AAAAAAAAHuA/lVCEFF8BaKcYjsVe5Znzb_EdqE34Xo72gCLcBGAs/s1600/bar.PNG](https://1.bp.blogspot.com/-bamSdPlBdas/XRD7aKeEgSI/AAAAAAAAHuA/lVCEFF8BaKcYjsVe5Znzb_EdqE34Xo72gCLcBGAs/s1600/bar.PNG)

If you are using **Jupyter Notebook**, you can submit this command  `%matplotlib inline`  **once** to display or show plots automatically without need to enter `plt.show()` after generation of each plot.

## Functions used for different types of plots

The following tables explain different graphs along with functions defined for these graphs in matplotlib library.

## 1. Bar Graph

Bar Graph is used to make comparison between different categories or groups. Suppose you want to show comparison between cities in terms of average annual income. Let's try with basic bar chart.

```
plt.title("Simple Bar graph") # Name title of the graph
plt.xlabel('Students') # Assign the name of the x axis
plt.ylabel("Math Score") # Assign the name of the y axis
plt.bar(x, y, color='red') # Change bar color
plt.show()

```

![https://4.bp.blogspot.com/-4l68qngHTco/XREK_FNGlUI/AAAAAAAAHuM/60tOwItGLckfm-3RiyTVzddue06QCUMvgCLcBGAs/s1600/bar_2.PNG](https://4.bp.blogspot.com/-4l68qngHTco/XREK_FNGlUI/AAAAAAAAHuM/60tOwItGLckfm-3RiyTVzddue06QCUMvgCLcBGAs/s1600/bar_2.PNG)

You can style your graph using the following functions -

- `plt.title( )` for specifying title of your plot.
- `plt.xlabel( )` for labeling x-axis.
- `plt.ylabel( )` for labeling y-axis.
- `color =`  option in plt.bar( ) for defining color of bars.

**How to show values or labels on top of bar**

It's not easy and straightforward to show values on bar graph as there is no in-built function for this task in matplotlib library. Hence we have to write our code to accomplish this task.

```
barplot = plt.bar(x, y)
for bar in barplot:
    yval = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2.0, yval, int(yval), va='bottom') #va: vertical alignment y positional argument

plt.title("Simple Bar graph")
plt.xlabel('Students')
plt.ylabel("Math Score")

```

![https://1.bp.blogspot.com/-pUHtZfGxXvE/XREP4YBpL0I/AAAAAAAAHuY/Z0ULaxpskSwtzs-DFA9Kwv0e16IaAvQkACLcBGAs/s1600/bar_3.PNG](https://1.bp.blogspot.com/-pUHtZfGxXvE/XREP4YBpL0I/AAAAAAAAHuY/Z0ULaxpskSwtzs-DFA9Kwv0e16IaAvQkACLcBGAs/s1600/bar_3.PNG)

How this code works?

We need to understand the logic for showing labels on top of each bar. First we need to find out the position where we need to show the labels.

```
.get_height()
```

returns height of rectangle of each bar which is basically a value of y-axis. To find value of x-axis, we can use

```
get_x()
```

and

```
get_width()
```

function.

```
plt.text()
```

is used to place text on the graph.

**Syntax of plt.text( )**

```
plt.text(position of x axis where you want to show text, position of y-axis, text, other_options)
```

*We used int(yval) instead of yval because by default, it shows values in decimals.*

**How to hide axis**

Many times we hide y-axis to give aesthetic touch to our bar graph. To do this in matplotlib, we can leverage

```
plt.yticks( )
```

function.

```
[ ]
```

means empty list.

```
plt.yticks([])

```

![https://1.bp.blogspot.com/-YvqTPQJiSIc/XRIJNWaAMjI/AAAAAAAAHvM/G7--GNNpAM8DZtk4TxFSuZgxL-y95keIwCLcBGAs/s1600/bar_4.PNG](https://1.bp.blogspot.com/-YvqTPQJiSIc/XRIJNWaAMjI/AAAAAAAAHvM/G7--GNNpAM8DZtk4TxFSuZgxL-y95keIwCLcBGAs/s1600/bar_4.PNG)

How to show string values in Bar Graph

It is straightforward to do if you are using

**matplotlib version 2.1**

onwards. To check version of python package, you can use

```
!pip show matplotlib
```

in Jupyter notebook. To upgrade it, you can submit the code

```
!pip install --upgrade matplotlib
```

```
x = ['A', 'B', 'C', 'D', 'E']
y = [5, 7, 3, 8, 4]
plt.bar(x, y)

```

If you are using version prior to matplotlib 2.1, matplotlib does not take string values in x-axis in bar graph so we need to find workaround to solve this problem. Solution is to show string values as labels and range(len(x)) would display values through 1 to 5 in x-axis. plt.xticks can be used for this task. It follows the syntax `plt.xticks(location of ticks, labels, size='small')`

`plt.bar(range(len(x)), y)
plt.xticks(range(len(x)), x, size='small')`

**Horizontal Bar Chart**

Nowadays analysts prefer showing horizontal bar chart instead of column bar chart for comparison as it looks more professional and elegant in terms  of look. Both the type of charts serve the same purpose.

```
plt.barh(x,y)
```

is used for generating horizontal bar graph.

```
plt.barh(x,y)
plt.title("Simple Horizontal Bar graph")
plt.xlabel("Math Score")
plt.ylabel('Students')

```

![https://1.bp.blogspot.com/-yqMjCXJX5Yk/XRJF1XK49mI/AAAAAAAAHvo/jeo9A4Bv7AIBTNRBLSMpg9mv5QEMfkbBACLcBGAs/s1600/bar_5.PNG](https://1.bp.blogspot.com/-yqMjCXJX5Yk/XRJF1XK49mI/AAAAAAAAHvo/jeo9A4Bv7AIBTNRBLSMpg9mv5QEMfkbBACLcBGAs/s1600/bar_5.PNG)

**How to sort or order bars**

To arrange bars in order based on values not alphabetically, we need to combine both the lists and then sort them based on value of list y.

```
zip( )
```

function is used to combine items of lists x and y.

```
sorted( )
```

sort them based on y. Then we split and store it in x and y lists.

```
y,x = zip(*sorted(zip(y,x)))
plt.barh(x,y)

```

![https://1.bp.blogspot.com/-aXGRcU6QbGg/XRJPbgbjPYI/AAAAAAAAHv0/TwYCWxznKYsGhfOKQW8M1BF5kFlgnqpYgCLcBGAs/s1600/bar_6.PNG](https://1.bp.blogspot.com/-aXGRcU6QbGg/XRJPbgbjPYI/AAAAAAAAHv0/TwYCWxznKYsGhfOKQW8M1BF5kFlgnqpYgCLcBGAs/s1600/bar_6.PNG)

Reverse order of bars

```
plt.subplot()
```

is used to find out current axes and then invert function assists to reverse the order.

```
plt.barh(x,y)
ax=plt.subplot()
ax.invert_yaxis()

```

**Use Professional Themes / Styles for Graphs**

There are many themes available in pyplot module. See the list of built-in themes which you can leverage to make your graph more graceful.

```
print(plt.style.available)

```

```
['bmh', 'classic', 'dark_background', 'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid', 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks', 'seaborn-white', 'seaborn-whitegrid', 'seaborn', '_classic_test']

```

I'm going to use

```
fivethirtyeight
```

theme.

```
plt.style.use('fivethirtyeight')

```

![https://1.bp.blogspot.com/-J-pfse_rKmA/XRJtoHZvpiI/AAAAAAAAHwU/rTQEG-VOl-su1ajqZu6KGqTX7v289PwlQCLcBGAs/s1600/Bar%2BProfessional%2BTheme.PNG](https://1.bp.blogspot.com/-J-pfse_rKmA/XRJtoHZvpiI/AAAAAAAAHwU/rTQEG-VOl-su1ajqZu6KGqTX7v289PwlQCLcBGAs/s1600/Bar%2BProfessional%2BTheme.PNG)

## Line Graph

Line graphs are used to show value of some items over time. Suppose you need to show pass percentage of students of government schools in the last 5 years. Another example - how sales have changed in the past five years? Let's create a

[pandas](https://www.listendata.com/2017/12/python-pandas-tutorial.html)

dataframe for the same.

```
import pandas as pd

df = pd.DataFrame({"Year" : [2014,2015,2016,2017,2018],
                  "Sales" : [2000, 3000, 4000, 3500, 6000]})

```

```
plt.plot( )
```

function is used for line graph. It is the default graph type.

```
# plot line chart
plt.plot(df["Year"], df["Sales"])
plt.title("Simple Line Plot")
plt.xlabel('Year')
plt.ylabel('Sales')

```

![https://1.bp.blogspot.com/-Q9Z9b6_4tB4/XRJz8Xr0jRI/AAAAAAAAHwg/NkMjtUP9qkQND2HtlyjVeVTvVClwdciHACLcBGAs/s1600/lineplot.PNG](https://1.bp.blogspot.com/-Q9Z9b6_4tB4/XRJz8Xr0jRI/AAAAAAAAHwg/NkMjtUP9qkQND2HtlyjVeVTvVClwdciHACLcBGAs/s1600/lineplot.PNG)

Pandas can make graphs by calling plot directly from the data frame. Plot can be called by defining plot type in `kind=` option.

Syntax of Plot in Pandas

`df.plot(x="Year", y="Sales", kind="line")`

`- 'line' for line plot (Default)
- 'bar'  for vertical bar plots
- 'barh' for horizontal bar plots
- 'hist' for histogram
- 'pie' for pie plots
- 'box' for boxplot
- 'kde' for density plots
- 'area' for area plots
- 'scatter' for scatter plots
- 'hexbin' for hexagonal bin plots`

**Add Marker in Line Plot**

By making use of

**style=**

option, you can include marker with customization in color and style.

```
ax = df.plot(x="Year", y="Sales", kind="line", title ="Simple Line Plot", legend=False, style = 'r--')
ax.set(ylabel='Sales', xlabel = 'Year', xticks =df["Year"])

```

![https://1.bp.blogspot.com/-hccNaXrlHMA/XRKBzwr4gJI/AAAAAAAAHww/9D8UtD91lAw3L735o6Pm-AOtYHxtjXdwgCLcBGAs/s1600/line_marker.PNG](https://1.bp.blogspot.com/-hccNaXrlHMA/XRKBzwr4gJI/AAAAAAAAHww/9D8UtD91lAw3L735o6Pm-AOtYHxtjXdwgCLcBGAs/s1600/line_marker.PNG)

You can also use these styles

```
ro, ro--, r+, rD-.
```

. They 
refer to cirles, dash lines, dash-dotted lines. You can mention any color ('g' for green, 'b' for blue, 'k' for black etc.)

`.set` method is used to add x and y axis labels, limits and ticks. It can also be written like the code below -

```
ax.set_ylabel('Sales')
ax.set_xlabel('Year')
ax.set_xticks(df["Year"])

```

Syntax of

**ax.set**

family functions is equivalent to

**plt.**

styling functions. See comparison of some of them -

```
ax.set_ylabel() plt.ylabel()
ax.set_xlabel() plt.xlabel()
ax.set_xticks() plt.xticks()

```

```
legend=False
```

tells pandas to turnoff legend

**Add Multiple Lines in Line Graph Pandas Way**

In the code below, we are creating a pandas DataFrame consisting sales of two products A and B along with time period (Year). Idea is to compare sales of products and how they performed in the last 5 years.

```
import pandas as pd

product = pd.DataFrame({"Year" : [2014,2015,2016,2017,2018],
                  "ProdASales" : [2000, 3000, 4000, 3500, 6000],
                  "ProdBSales" : [3000, 4000, 3500, 3500, 5500]})

# Multi line plot
ax = product.plot("Year", "ProdASales", kind="line", label = 'Product A Sales')
product.plot("Year", "ProdBSales", ax= ax , kind="line", label = 'Product B Sales', title= 'MultiLine Plot') #ax : axes object

# Set axes
ax.set(ylabel='Sales', xlabel = 'Year', xticks =df["Year"])

```

![https://1.bp.blogspot.com/-GrMq0C9A6Lw/XRKFC_sjvrI/AAAAAAAAHxA/bhAJxG0FRf0XCXJ7evomyth-ou4IxhCCgCLcBGAs/s1600/multiline.PNG](https://1.bp.blogspot.com/-GrMq0C9A6Lw/XRKFC_sjvrI/AAAAAAAAHxA/bhAJxG0FRf0XCXJ7evomyth-ou4IxhCCgCLcBGAs/s1600/multiline.PNG)

> We included second line by adding it in
> 
> 
> ```
> ax=
> ```
> 

**How to change interval on x axis?**

Suppose you want to show years from 2014 to 2018 with increment by an year on x-axis. If values are incremented by 0.5 instead of 1 so that's an issue you should fix it. See the image below -

![https://2.bp.blogspot.com/-YWwfC56b0nI/XRSoHN9db0I/AAAAAAAAHxM/_rGXl02G0bswLBQykag-RsGlFq6MDwm1ACLcBGAs/s1600/line_interval.PNG](https://2.bp.blogspot.com/-YWwfC56b0nI/XRSoHN9db0I/AAAAAAAAHxM/_rGXl02G0bswLBQykag-RsGlFq6MDwm1ACLcBGAs/s1600/line_interval.PNG)

```
# How to show years with same interval as it is defined in column
ax = df.plot(x="Year", y="Sales", kind="line", title ="Simple Line Plot", legend=False)
ax.set(ylabel='Sales', xlabel = 'Year',xticks =df["Year"])

```

`xticks=` can be used to change the scale of intervals of x axis. It will show the ticks what do you want to show on x axis.

## Scatter Plot

A scatter plot is mainly used to show relationship between two continuous variables. For example, you want to measure the relationship between height and weight. Like line graph, it can also be used to show trend over time. We generally plot a set of points on x and y axes.

`kind = 'scatter'` is used for creating scatter diagram.

```
ax = product.plot("Year", "ProdASales", kind='scatter', color = 'red', title = 'Year by ProductA Sales')
ax.set(ylabel='ProductA Sales', xlabel = 'Year', xticks =df["Year"])
plt.show()

```

![https://2.bp.blogspot.com/-c-WmsXX7SaU/XRTdl4EnTSI/AAAAAAAAHxw/ULSDTnmKh-QrOvxivgnS8vlJmH8p7GTYwCLcBGAs/s1600/Scatter.PNG](https://2.bp.blogspot.com/-c-WmsXX7SaU/XRTdl4EnTSI/AAAAAAAAHxw/ULSDTnmKh-QrOvxivgnS8vlJmH8p7GTYwCLcBGAs/s1600/Scatter.PNG)

## Pie Chart

A pie chart is a circular graph which splits data into slices to show numerical proportion of each category. If you are showing percentages, ll of them should add to 100%.

![https://3.bp.blogspot.com/-HExQW4_F88A/XRTmXjK44ZI/AAAAAAAAHx8/qccAeJTiv6Yt-5riYyk8A9grVfD3dC4oQCLcBGAs/s1600/pie_chart.PNG](https://3.bp.blogspot.com/-HExQW4_F88A/XRTmXjK44ZI/AAAAAAAAHx8/qccAeJTiv6Yt-5riYyk8A9grVfD3dC4oQCLcBGAs/s1600/pie_chart.PNG)

```
share = [20, 12, 11, 4, 3]
companies = ['Google', 'Facebook', 'Apple', 'Microsoft', 'IBM', ]
comp = pd.DataFrame({"share" : share, "companies" : companies})
ax = comp.plot(y="share", kind="pie", labels = comp["companies"], autopct = '%1.0f%%', legend=False, title='Market Share')

# Hide y-axis label
ax.set(ylabel='')

```

**Customize Pie Chart**

The default

**startangle**

is 0. By making

**startangle = 90**

, everything will be rotated counter-clockwise by 90 degrees. By using

**explode =**

option, you can explode specific categories. In the following program, we are exploding first three categories.

```
# Customize Pie Chart
ax = comp.plot(y="share", kind="pie", labels = comp["companies"], startangle = 90, shadow = True,
        explode = (0.1, 0.1, 0.1, 0, 0), autopct = '%1.0f%%', legend=False, title='Market Share')
ax.set(ylabel='')
plt.show()

```

## Histogram

Histogram is used to show the frequency distribution of a continuous variable. Suppose you want to see the distribution of marks got by students.

![https://1.bp.blogspot.com/-ZRp4gvLfEBo/XRT93GoozBI/AAAAAAAAHyM/nOmLgLaZS5ABatepl3BqrPVmUekVNgY4ACLcBGAs/s1600/Histogram.PNG](https://1.bp.blogspot.com/-ZRp4gvLfEBo/XRT93GoozBI/AAAAAAAAHyM/nOmLgLaZS5ABatepl3BqrPVmUekVNgY4ACLcBGAs/s1600/Histogram.PNG)

```
# Creating random data
import numpy as np
np.random.seed(1)
mydf = pd.DataFrame({"Age" : np.random.randint(low=20, high=100, size=50)})

# Histogram
ax = mydf.plot(bins= 5, kind="hist", rwidth = 0.7, title = 'Distribution - Marks', legend=False)
ax.set(xlabel="Bins")
plt.show()

```

**bins**

represents the number of intervals you want to show on x axis.

**rwidth**

shows the relative width of the bars as a fraction of the bin width.

## How to add multiple sub-plots

With the use of matplotlib library, we can generate multiple sub-plots in the same graph or figure. Matplotlib provides two interfaces to do this task -

```
plt.subplots( )
```

and

```
plt.figure()
```

. Logic is similar in both the ways - we will have a figure and we'll add multiple axes (sub-plots) on the figure one by one.

I created a dummy DataFrame for illustration. In this example, we have data for cities with cost of living scores (fake data!) of year 2017 and 2018.

```
labels = ['Delhi', 'Mumbai', 'Bangalore', 'Chennai']
x1 = [45, 30, 15, 10]
x2 = [25, 20, 25, 50]

finaldf = pd.DataFrame({"2017_Score":x1, "2018_Score" : x2, "cities" : labels})

```

`.add_subplot() or .subplots()` follows the syntax rule -
subplot(number of rows, number of columns, plot number)
.add_subplot(121) means 1 row, 2 columns and 1st plot
.add_subplot(122) means 1 row, 2 columns and 2nd plot
Similarly, .subplots(1, 2) means 1 row and 2 columns

Both the following methods return same result. It generate two sub-plots and place them next to each other (horizontally).

**Method I**

`fig = plt.figure()

ax1 = fig.add_subplot(121)
ax = finaldf.plot(x="cities",  y="2017_Score", ax=ax1, kind="barh", legend = False, title = "2017 Score")
ax.invert_yaxis()

ax2 = fig.add_subplot(122)
ax = finaldf.plot(x="cities",  y="2018_Score", ax=ax2, kind="barh", legend = False, title = "2018 Score")
ax.invert_yaxis()
ax.set(ylabel='')`

**Method II**

`fig, (ax0, ax01) = plt.subplots(1, 2)

ax = finaldf.plot(x="cities",  y="2017_Score", ax=ax0, kind="barh", legend = False, title = "2017 Score")
ax.invert_yaxis()

ax = finaldf.plot(x="cities",  y="2018_Score", ax=ax01, kind="barh", legend = False, title = "2018 Score")
ax.invert_yaxis()
ax.set(ylabel='')`

![https://4.bp.blogspot.com/-rNHd8y_wbsI/XRUsnjf8PKI/AAAAAAAAHzU/w-VTTPhEA6AhNHklRtOsfhNd03SyOL9xwCLcBGAs/s1600/multiplot.PNG](https://4.bp.blogspot.com/-rNHd8y_wbsI/XRUsnjf8PKI/AAAAAAAAHzU/w-VTTPhEA6AhNHklRtOsfhNd03SyOL9xwCLcBGAs/s1600/multiplot.PNG)

Detailed Explanation

These 3 lines of code return blank (empty) 2 sub-plots. 121 refers to left hand side plot and 122 refers to right hand side plot. With the use of

**ax=**

object we use axes and control positioning of sub-plots.

```
fig = plt.figure()
fig.add_subplot(121)
fig.add_subplot(122)

```

How to show sub-plots vertically

In this section, we will demonstrate how to put a sub-plot on top of second one. Here we are using

**211**

and

**222**

in subplot( ) function. 211 means 2 rows, 1 column and 1st plot.

```
fig = plt.figure()
ax1 = fig.add_subplot(211)
ax = finaldf.plot(x="cities",  y="2017_Score", ax=ax1, kind="barh", legend = False, title = "2017 vs 2018 Score")
ax.invert_yaxis()
plt.xticks(range(0,60,10))
ax.set(ylabel='')

ax2 = fig.add_subplot(212)
ax = finaldf.plot(x="cities",  y="2018_Score", ax=ax2, kind="barh", legend = False)
ax.invert_yaxis()
ax.set(ylabel='')

```

![https://1.bp.blogspot.com/-MGPmG4e1Hk0/XRUy7JY-ZSI/AAAAAAAAHzg/DrLGoY-XTy0WSQrEbN9h3OVVVJSyM7mBwCLcBGAs/s1600/multiplot2.PNG](https://1.bp.blogspot.com/-MGPmG4e1Hk0/XRUy7JY-ZSI/AAAAAAAAHzg/DrLGoY-XTy0WSQrEbN9h3OVVVJSyM7mBwCLcBGAs/s1600/multiplot2.PNG)

## Useful Tips

How to save plot

```
# save plot
x = ['A','B','C', 'D']
y = [1,2,3,4]
fig = plt.figure()
plt.bar(x, y)
fig.savefig('C:/My Files/Blog/firstimg.png')
plt.close(fig)

```

How to set different limits in axis Suppose you have a bar graph and you want to set limits in x and y axis manually.

```
plt.subplot()
```

returns axes. In

```
set_ylim( )
```

, you can assign limits which is smallest and largest value of y axis. Similarly you can set limit in x-axis.

```
x = ['A','B','C', 'D']
y = [100,119,800,900]
plt.bar(x, y)
ax = plt.subplot()
ax.set_ylim(0,1000)
plt.show()

```

How to show multiple entries in legend

```
plt.legend(["First","Second"])

```

How to change font size, weight and color in graph

```
plt.bar(x, y)
plt.title("Cost of Living", fontsize=18, fontweight='bold', color='blue')
plt.xlabel("Cities", fontsize=16)
plt.ylabel("Score", fontsize=16)

```

Exercise

Get your hands dirty with this exercise. Prepare the graph shown below using dataframe

```
finaldf
```

. Give attention to each part of the graph and try to replicate it. Post your solution in the comment box below.

![https://4.bp.blogspot.com/-tGl4a8jkt7U/XRXewT_SYvI/AAAAAAAAHz4/QfkCWeNvWHo6NekJKY35ytEK30HaXShoACLcBGAs/s1600/exercise.PNG](https://4.bp.blogspot.com/-tGl4a8jkt7U/XRXewT_SYvI/AAAAAAAAHz4/QfkCWeNvWHo6NekJKY35ytEK30HaXShoACLcBGAs/s1600/exercise.PNG)

EndNote

I hope this article gave you a fair idea about matplotlib library and how to generate plots with customization in python. Your next step should be practice, practice and practice with some sample or publicly available datasets (available on UCI Machine Learning Repository and 
kaggle websites).
# Filter

To

**filter**

only those rows which have Index as "A" we write:

```
income[income.Index == "A"]

#Alternatively
income.loc[income.Index == "A",:]
```

```
  Index     State    Y2002    Y2003    Y2004    Y2005    Y2006    Y2007  \
0     A   Alabama  1296530  1317711  1118631  1492583  1107408  1440134
1     A    Alaska  1170302  1960378  1818085  1447852  1861639  1465841
2     A   Arizona  1742027  1968140  1377583  1782199  1102568  1109382
3     A  Arkansas  1485531  1994927  1119299  1947979  1669191  1801213
     Y2008    Y2009    Y2010    Y2011    Y2012    Y2013    Y2014    Y2015
0  1945229  1944173  1237582  1440756  1186741  1852841  1558906  1916661
1  1551826  1436541  1629616  1230866  1512804  1985302  1580394  1979143
2  1752886  1554330  1300521  1130709  1907284  1363279  1525866  1647724
3  1188104  1628980  1669295  1928238  1216675  1591896  1360959  1329341

```

To select the States having Index as "A":

```
income.loc[income.Index == "A","State"]
income.loc[income.Index == "A",:].State
```

To filter the rows with Index as "A" and income for 2002 > 1500000"

```
income.loc[(income.Index == "A") & (income.Y2002 > 1500000),:]
```

To filter the rows with index either "A" or "W", we can use

**isin( )**

function:

```
income.loc[(income.Index == "A") | (income.Index == "W"),:]

#Alternatively.
income.loc[income.Index.isin(["A","W"]),:]
```

```
   Index          State    Y2002    Y2003    Y2004    Y2005    Y2006    Y2007  \
0      A        Alabama  1296530  1317711  1118631  1492583  1107408  1440134
1      A         Alaska  1170302  1960378  1818085  1447852  1861639  1465841
2      A        Arizona  1742027  1968140  1377583  1782199  1102568  1109382
3      A       Arkansas  1485531  1994927  1119299  1947979  1669191  1801213
47     W     Washington  1977749  1687136  1199490  1163092  1334864  1621989
48     W  West Virginia  1677347  1380662  1176100  1888948  1922085  1740826
49     W      Wisconsin  1788920  1518578  1289663  1436888  1251678  1721874
50     W        Wyoming  1775190  1498098  1198212  1881688  1750527  1523124
      Y2008    Y2009    Y2010    Y2011    Y2012    Y2013    Y2014    Y2015
0   1945229  1944173  1237582  1440756  1186741  1852841  1558906  1916661
1   1551826  1436541  1629616  1230866  1512804  1985302  1580394  1979143
2   1752886  1554330  1300521  1130709  1907284  1363279  1525866  1647724
3   1188104  1628980  1669295  1928238  1216675  1591896  1360959  1329341
47  1545621  1555554  1179331  1150089  1775787  1273834  1387428  1377341
48  1238174  1539322  1539603  1872519  1462137  1683127  1204344  1198791
49  1980167  1901394  1648755  1940943  1729177  1510119  1701650  1846238
50  1587602  1504455  1282142  1881814  1673668  1994022  1204029  1853858

```

Alternatively we can use

```
query( )
```

function which also eliminates the need to specify data frame while mentioning column(s) and
 lets you write our filtering criteria:

```
income.query('Y2002>1700000 & Y2003 > 1500000')
```

# Examples of Data Filtering

It is one of the most initial step of data preparation for predictive modeling or any reporting project. It is also called 'Subsetting Data'.  See some of the examples of data filtering below.

- Select all the active customers whose accounts were opened after 1st January 2019
- Extract details of all the customers who made more than 3 transactions in the last 6 months
- Fetch information of employees who spent more than 3 years in the organization and received highest rating in the past 2 years
- Analyze complaints data and identify customers who filed more than 5 complaints in the last 1 year
- Extract details of metro cities where per capita income is greater than 40K dollars

### Import Data

Make sure

[pandas package](https://www.listendata.com/2017/12/python-pandas-tutorial.html)

is already installed before submitting the following code. You can check it by running

```
!pip show pandas
```

statement in Ipython console. If it is not installed, you can install it by using the command

```
!pip install pandas
```

.

We are going to use dataset containing details of flights departing from NYC in 2013. This dataset has 336776 rows and 16 columns. See column names below. To import dataset, we are using `read_csv( )` function from pandas package.

```
['year', 'month', 'day', 'dep_time', 'dep_delay', 'arr_time',
       'arr_delay', 'carrier', 'tailnum', 'flight', 'origin', 'dest',
       'air_time', 'distance', 'hour', 'minute']

```

```
import pandas as pd
df = pd.read_csv("https://raw.githubusercontent.com/JackyP/testing/master/datasets/nycflights.csv", usecols=range(1,17))

```

## Filter pandas dataframe by column value

Select flights details of JetBlue Airways that has 2 letters carrier code `B6` with origin from `JFK` airport

### Method 1 : DataFrame Way

```
newdf = df[(df.origin == "JFK") & (df.carrier == "B6")]

```

```
newdf.head()
Out[23]:
    year  month  day  dep_time  ...  air_time  distance  hour minute
3   2013      1    1     544.0  ...     183.0      1576   5.0   44.0
8   2013      1    1     557.0  ...     140.0       944   5.0   57.0
10  2013      1    1     558.0  ...     149.0      1028   5.0   58.0
11  2013      1    1     558.0  ...     158.0      1005   5.0   58.0
15  2013      1    1     559.0  ...      44.0       187   5.0   59.0

[5 rows x 16 columns]

```

1. Filtered data (after subsetting) is stored on new dataframe called `newdf`.
2. Symbol `&` refers to `AND` condition which means meeting both the criteria.
3. This part of code `(df.origin == "JFK") & (df.carrier == "B6")` returns True / False. True where condition matches and False where the
condition does not hold. Later it is passed within df and returns all
the rows corresponding to **True**. It returns 4166 rows.

### Method 2 : Query Function

In pandas package, there are multiple ways to perform filtering. The 
above code can also be written like the code shown below. This method is
 elegant and more readable and you don't need to mention dataframe name 
everytime when you specify columns (variables).

```
newdf = df.query('origin == "JFK" & carrier == "B6"')

```

[How to pass variables in query function](https://www.listendata.com/2020/12/how-to-use-variable-in-query-in-pandas.html)

Method 3 : loc function

loc is an abbreviation of

**location**

term. All these 3 methods return same output. It's just a different ways of doing filtering rows.

```
newdf = df.loc[(df.origin == "JFK") & (df.carrier == "B6")]

```

## Filter Pandas Dataframe by Row and Column Position

Suppose you want to select specific rows by their position (let's say from second through fifth row). We can use

```
df.iloc[ ]
```

function for the same.

> Indexing in python starts from zero. df.iloc[0:5,] refers to first to 
fifth row (excluding end point 6th row here). df.iloc[0:5,] is 
equivalent to df.iloc[:5,]
> 

```
df.iloc[:5,] #First 5 rows
df.iloc[1:5,] #Second to Fifth row
df.iloc[5,0] #Sixth row and 1st column
df.iloc[1:5,0] #Second to Fifth row, first column
df.iloc[1:5,:5] #Second to Fifth row, first 5 columns
df.iloc[2:7,1:3] #Third to Seventh row, 2nd and 3rd column

```

Difference between loc and iloc function

**loc**

considers rows based on index labels. Whereas

**iloc**

considers rows based on position in the index so it only takes integers.

Let's create a sample data for illustration

```
import numpy as np
x = pd.DataFrame({"col1" : np.arange(1,20,2)}, index=[9,8,7,6,0, 1, 2, 3, 4, 5])

```

```
    col1
9      1
8      3
7      5
6      7
0     9
1     11
2     13
3     15
4     17
5     19

```

**iloc - Index Position**

`x.iloc[0:5]

**Output**
   col1
9     1
8     3
7     5
6     7
0     9`
*Selecting rows based on index or row position*

**loc - Index Label**

`x.loc[0:5]

**Output**
   col1
0     9
1    11
2    13
3    15
4    17
5    19`
*Selecting rows based on labels of index*

**How `x.loc[0:5]` returns 6 rows (inclusive of 5 which is 6th element)?**

It is because `loc` does not produce output based on 
index position. It considers labels of index only which can be alphabet 
as well and includes both starting and end point. Refer the example 
below.

```
x = pd.DataFrame({"col1" : range(1,5)}, index=['a','b','c','d'])
x.loc['a':'c'] # equivalent to x.iloc[0:3]

   col1
a     1
b     2
c     3

```

## Filter pandas dataframe by rows position and column names

Here we are selecting first five rows of two columns named origin and dest.

```
df.loc[df.index[0:5],["origin","dest"]]

```

```
df.index
```

returns index labels. df.index[0:5] is required 
instead of 0:5 (without df.index) because index labels do not always in 
sequence and start from 0. It can start from any number or even can have
 alphabet letters. Refer the example where we showed comparison of iloc 
and loc.

## Selecting multiple values of a column

Suppose you want to include all the flight details where origin is either JFK or LGA.

```
# Long Way
newdf = df.loc[(df.origin == "JFK") | (df.origin == "LGA")]

# Smart Way
newdf = df[df.origin.isin(["JFK", "LGA"])]

```

```
|
```

implies OR condition which means any of the conditions holds True.

```
isin( )
```

is similar to IN operator in SAS and R which can take many values and 
apply OR condition. Make sure you specify values in list [ ].

## Select rows whose column value does not equal a specific value

In this example, we are deleting all the flight details where origin is from JFK.

```
!=
```

implies NOT EQUAL TO.

```
newdf = df.loc[(df.origin != "JFK") & (df.carrier == "B6")]
```

Let's check whether the above line of code works fine or not by looking at unique values of column origin in newdf.

```
pd.unique(newdf.origin)

['LGA', 'EWR']

```

## How to negate the whole condition

Tilde

```
~
```

is used to negate the condition. It is equivalent to NOT operator in SAS and R.

```
newdf = df[~((df.origin == "JFK") & (df.carrier == "B6"))]

```

## Select Non-Missing Data in Pandas Dataframe

With the use of

```
notnull()
```

function, you can exclude or 
remove NA and NAN values. In the example below, we are removing missing 
values from origin column. Since this dataframe does not contain any 
blank values, you would find same number of rows in newdf.

```
newdf = df[df.origin.notnull()]

```

## Filtering String in Pandas Dataframe

It is generally considered tricky to handle text data. But python makes 
it easier when it comes to dealing character or string columns. Let's 
prepare a fake data for example.

```
import pandas as pd
df = pd.DataFrame({"var1": ["AA_2", "B_1", "C_2", "A_2"]})

   var1
0  AA_2
1   B_1
2   C_2
3   A_2

```

Select rows having values starting from letter 'A'

By using

```
.str
```

, you can enable string functions and can apply on pandas dataframe.

**str[0]**

means first letter.

```
df[df['var1'].str[0] == 'A']
```

Filter rows having string length greater than 3

```
len( )
```

function calculates length of iterable.

```
df[df['var1'].str.len()>3]
```

Select string containing letters A or B

```
contains( )
```

function is similar to LIKE statement in SQL and SAS. You can subset data by mentioning pattern in contains( ) function.

```
df[df['var1'].str.contains('A|B')]

Output
   var1
0  AA_2
1   B_1
3   A_2

```

## Handle space in column name while filtering

Let's rename a column

**var1**

with a space in between

**var 1**

We can rename it by using

**rename**

function.

```
df.rename(columns={'var1':'var 1'}, inplace = True)
```

By using backticks

```
` `
```

we can include the column having space. See the example code below.

```
 newdf = df.query("`var 1` == 'AA_2'")
```

Backticks are supported from version **0.25** of pandas package. Run this command in console to check pandas version `!pip show pandas` If you have version **prior to the version 0.25** you can upgrade it by using this command `!pip install --upgrade pandas --user`

## How to filter data without using pandas package

You can perform filtering using pure python methods without dependency on pandas package.

Warning : Methods shown below for filtering are not efficient ones. The main objective of showing the following methods is to show how to do subsetting without using pandas package. In your live project, you should use pandas' builtin functions (query( ), loc[ ], iloc[ ]) which are explained above.

We don't need to create a dataframe to store data. We can stock it in list data structure.

```
lst_df
```

contains flights data which were imported from CSV file.

```
import csv
import requests

response = requests.get('https://dyurovsky.github.io/psyc201/data/lab2/nycflights.csv').text
lines = response.splitlines()
d = csv.DictReader(lines)
lst_df = list(d)

```

### Lambda Method for Filtering

Lambda is an alternative way of defining user defined function. With the use of lambda, you can define function in a single line of code. You can check out this

**[link](https://www.listendata.com/2019/04/python-lambda-function.html)**

to learn more about it.

```
l1 = list(filter(lambda x: x["origin"] == 'JFK' and x["carrier"] == 'B6', lst_df))

```

If you are wondering how to use this lambda function on a dataframe, you can submit the code below.

```
newdf = df[df.apply(lambda x: x["origin"] == 'JFK' and x["carrier"] == 'B6', axis=1)]

```

### List Comprehension Method for Filtering

List comprehension is an alternative to lambda function and makes code more readable.

**[Detailed Tutorial : List Comprehension](https://www.listendata.com/2019/07/python-list-comprehension-with-examples.html)**

```
l2 = list(x for x in lst_df if x["origin"] == 'JFK' and x["carrier"] == 'B6')

```

You can use list comprehension on dataframe like the way shown below.

```
newdf = df.iloc[[index for index,row in df.iterrows() if row['origin'] == 'JFK' and row['carrier'] == 'B6']]

```

### Create Class for Filtering

Python is an object-oriented programming language in which code is implemented using

```
class
```

.

```
class filter:
  def __init__(self, l, query):
    self.output = []
    for data in l:
      if eval(query):
        self.output.append(data)

l3 = filter(lst_df, 'data["origin"] == "JFK" and data["carrier"] == "B6"').output

```

```
x = df.loc[
    df.Country.eq("UK") & df.Type.isin(["A", "B", "C"]) & df.Cancelled.eq("N")
]
print(len(x))
```

```
mask = (
    df.Country.eq("UK") & df.Type.isin(["A", "B", "C"]) &
df.Cancelled.eq("N")
)

0     True
1    False
2     True
3     True
4    False
5    False
dtype: bool

```

```
x = df.loc[mask]

   Offer Country Type Cancelled
0    111      UK    A         N
2    333      UK    B         N
3    444      UK    C         N
```

`print(len(x))`

`my_count =len(df[(df.Country=='UK') && (df.Type in ['A','B','C']) && (df.Cancelled=='N')])`
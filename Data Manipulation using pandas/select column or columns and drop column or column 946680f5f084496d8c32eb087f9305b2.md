# select column or columns and drop column or columns/ Rename Columns / Select just numeric or categorical

Selecting only a few of the columns There are multiple ways you can select a particular column. Both the following line of code selects State variable from income data frame.

```
income["State"]
income.State

```

To select multiple columns by name, you can use the following syntax.

```
income[["Index","State","Y2008"]]
```

To select only specific columns and rows, we use either

**loc[ ]**

or

**iloc[ ]**

functions.
 The index or columns to be selected are passed as lists. 
"Index":"Y2008" denotes the that all the columns from Index to Y2008 are
 to be selected.

Syntax of df.loc[  ]

```
df.loc[row_index , column_index]
```

```
income.loc[:,["Index","State","Y2008"]]
income.loc[0:2,["Index","State","Y2008"]]  #Selecting rows with Index label 0 to 2 & columns
income.loc[:,"Index":"Y2008"]  #Selecting consecutive columns
#In the above command both Index and Y2008 are included.
income.iloc[:,0:5]  #Columns from 1 to 5 are included. 6th column not included
```

Difference between loc and iloc

**loc**

considers rows (or columns) with particular labels from the index. Whereas

**iloc**

considers rows (or columns) at particular positions in the index so

**it only takes integers**

.

```
x = pd.DataFrame({"var1" : np.arange(1,20,2)}, index=[9,8,7,6,10, 1, 2, 3, 4, 5])
```

```
    var1
9      1
8      3
7      5
6      7
10     9
1     11
2     13
3     15
4     17
5     19

```

- iloc Code
- loc code

```sql
x.iloc[:3]
Output:
   var1
9     1
8     3
7     5
```

```
x.loc[:3]
Output:
    var1
9      1
8      3
7      5
6      7
10     9
1     11
2     13
3     15
```

## Drop a column in python

In pandas,

```
drop( )
```

function is used to remove column(s).

```
axis=1
```

tells Python that you want to apply function on columns instead of rows.

```
df.drop(['A'], axis=1)
```

Column A has been removed. See the output shown below.

```
          B         C         D
0 -1.656038  1.655995 -1.413243
1  0.710933 -1.335381  0.832619
2 -0.411327  0.098119  0.768447
3 -0.093217  1.077528  0.196891
4  0.302687  0.125881 -0.665159
5 -0.692847 -1.463154 -0.707779

```

In order to create a

**new dataframe**

```
newdf
```

storing remaining columns, you can use the command below.

```
newdf = df.drop(['A'], axis=1)
```

To delete the column permanently from original dataframe

```
df
```

, you can use the option

```
inplace=True
```

```
df.drop(['A'], axis=1, inplace=True)

```

```
#Check columns in df after dropping column A
df.columns

Output
Index(['B', 'C', 'D'], dtype='object')

```

The parameter `inplace=` can be deprecated (removed) in 
future which means you might not see it working in the upcoming release 
of pandas package. You should avoid using this parameter if you are not 
already habitual of using it. Instead you can store your data after 
removing columns in a new dataframe (as explained in the above section).
 If you want to change the existing dataframe, try this  `df = df.drop(['A'], axis=1)`

## Remove Multiple Columns in Python

You can specify all the columns you want to remove in a list and pass it in

```
drop( )
```

function.

**Method I**

`df2 = df.drop(['B','C'], axis=1)`

**Method II**

`cols = ['B','C']
df2 = df.drop(cols, axis=1)`

### Select or Keep Columns

If you wish to select a column (instead of drop), you can use the command

```
df['A']
```

To select multiple columns, you can submit the following code.

```
df[['A','B']]
```

## How to drop column by position number from pandas Dataframe?

You can find out name of

**first column**

by using this command

```
df.columns[0]
```

. Indexing in python starts from 0.

```
df.drop(df.columns[0], axis =1)

```

To drop multiple columns by position (first and third columns), you can specify the position in list

```
[0,2]
```

.

```
cols = [0,2]
df.drop(df.columns[cols], axis =1)

```

## Drop columns by name pattern

```
df = pd.DataFrame({"X1":range(1,6),"X_2":range(2,7),"YX":range(3,8),"Y_1":range(2,7),"Z":range(5,10)})
```

```
   X1  X_2  YX  Y_1  Z
0   1    2   3    2  5
1   2    3   4    3  6
2   3    4   5    4  7
3   4    5   6    5  8
4   5    6   7    6  9

```

### Drop column whose name starts with letter 'X'

```
df.loc[:,~df.columns.str.contains('^X')]

```

How it works?

1. `^X` is a expression of regex language which refers to beginning of letter 'X'
2. `df.columns.str.contains('^X')` returns array [True, True, False, False, False]. True where condition meets. Otherwise False
3. Sign `~` refers to negate the condition.
4. `df.loc[ ]` is used to select columns

It can also be written like :

```
df.drop(df.columns[df.columns.str.contains('^X')], axis=1)
```

Other Examples

```
#Removing columns whose name contains string 'X'
df.loc[:,~df.columns.str.contains('X')]

#Removing columns whose name contains string either 'X' or 'Y'
df.loc[:,~df.columns.str.contains('X|Y')]

#Removing columns whose name ends with string 'X'
df.loc[:,~df.columns.str.contains('X$')]

```

### Drop columns where percentage of missing values is greater than 50%

```
df = pd.DataFrame({'A':[1,3,np.nan,5,np.nan],
                   'B':[4,np.nan,np.nan,5,np.nan]
                   })

```

% of missing values can be calculated by mean of NAs in each column.

```
cols = df.columns[df.isnull().mean()>0.5]
df.drop(cols, axis=1)

```

## Rename

If all the columns are to be renamed then we can use

**data.columns**

and assign the list of new column names.

```
#Renaming all the variables.
data.columns = ['Names','Zodiac Signs']
```

```
   Names Zodiac Signs
0   John        Libra
1   Mary    Capricorn
2  Julia        Aries
3  Kenny      Scorpio
4  Henry     Aquarius

```

If only some of the variables are to be renamed then we can use **rename( )** function where the new names are passed in the form of a dictionary.

```
#Renaming only some of the variables.
data.rename(columns = {"Names":"Cust_Name"},inplace = True)
```

```
  Cust_Name Zodiac Signs
0      John        Libra
1      Mary    Capricorn
2     Julia        Aries
3     Kenny      Scorpio
4     Henry     Aquarius

```

By default in pandas **inplace = False** which means that no changes are made in the original dataset. Thus if we wish to alter the original dataset we need to define **inplace = True**.

Suppose we want to replace only a particular character in the list of the column names then we can use **str.replace( )** function. For example, renaming the variables which contain "Y" as "Year"

```
income.columns = income.columns.str.replace('Y' , 'Year ')
income.columns
```

```
Index(['Index', 'State', 'Year 2002', 'Year 2003', 'Year 2004', 'Year 2005',
       'Year 2006', 'Year 2007', 'Year 2008', 'Year 2009', 'Year 2010',
       'Year 2011', 'Year 2012', 'Year 2013', 'Year 2014', 'Year 2015'],
      dtype='object')

```

### 2 Methods to rename columns in Pandas

In Pandas there are two simple methods to rename name of columns.

First step is to install [pandas package](https://www.listendata.com/2017/12/python-pandas-tutorial.html) if it is not already installed. You can check if the package is installed on your machine by running `!pip show pandas` statement in Ipython console. If it is not installed, you can install it by using the command `!pip install pandas`.

### Import Dataset for practice

To import dataset, we are using `read_csv( )` function from pandas package.

```
import pandas as pd
df = df = pd.read_csv("https://raw.githubusercontent.com/JackyP/testing/master/datasets/nycflights.csv", usecols=range(1,17))

```

To see the names of columns in a data frame, write the command below :

```
df.columns

```

```
Index(['year', 'month', 'day', 'dep_time', 'dep_delay', 'arr_time',
       'arr_delay', 'carrier', 'tailnum', 'flight', 'origin', 'dest',
       'air_time', 'distance', 'hour', 'minute'],
      dtype='object')

```

Method I : rename() function

Suppose you want to replace column name

```
year
```

with

```
years
```

. In the code below it will create a new dataframe named

```
df2
```

having new column names and same values.

```
df2 = df.rename(columns={'year':'years'})
```

If you want to make changes in the same dataset

```
df
```

you can try this option

**inplace = True**

```
df.rename(columns={'year':'years'}, inplace = True)
```

By default

**inplace = False**

is set, hence you need to specify this option and mark it True.
  
If you want to rename names of multiple columns, you can specify other columns with comma separator.

```
df.rename(columns={'year':'years', 'month':'months' }, inplace = True)

```

Method II : dataframe.columns = [list]

You can also assign the list of new column names to df.columns. See the 
example below. We are renaming year and month columns here.

```
df.columns = ['years', 'months', 'day', 'dep_time', 'dep_delay', 'arr_time',
       'arr_delay', 'carrier', 'tailnum', 'flight', 'origin', 'dest',
       'air_time', 'distance', 'hour', 'minute']

```

Rename columns having pattern Suppose you want to rename columns having underscore

**'_'** in their names. You want to get rid of

**underscore**

```
df.columns = df.columns.str.replace('_' , '')
```

New column names are as follows. You can observe no underscore in the column names.

```
  Index(['year', 'month', 'day', 'deptime', 'depdelay', 'arrtime', 'arrdelay',
       'carrier', 'tailnum', 'flight', 'origin', 'dest', 'airtime', 'distance',
       'hour', 'minute'],
      dtype='object')

```

### Rename columns by Position

If you want to change the name of column by position (for example renaming first column) you can do it by using the code below.

```
df.columns[0]
```

refers to first column.

```
df.rename(columns={ df.columns[0]: "Col1" }, inplace = True)

```

Rename columns in sequence If you want to change the name of column in sequence of numbers you can do it by iterating via

**for loop**

.

```
df.columns=["Col"+str(i) for i in range(1, 17)]
```

In the code below

```
df.shape[1]
```

returns no. of columns in the dataframe. We need to add 1 here as

```
range(1,17)
```

returns 1, 2, 3 through 16 (excluding 17).

```
df.columns=["Col"+str(i) for i in range(1, df.shape[1] + 1)]
```

Add prefix / suffix in column names

In case you want to add some text before or after existing column names, you can do it by using

```
add_prefix( )
```

and

```
add_suffix( )
```

functions.

```
df = df.add_prefix('V_')
df = df.add_suffix('_V')

```

How to access columns having space in names

For demonstration purpose we can add space in some column names by using

```
df.columns = df.columns.str.replace('_' , ' ')
```

. You can access the column using the syntax df["columnname"]

```
df["arr delay"]
```

### How to change row names

With the use of index option, you can rename rows (or index). In the 
code below, we are altering row names 0 and 1 to 'First' and 'Second' in
 dataframe df. By creating dictionary and taking previous row names as 
keys and new row names as values.

```
df.rename(index={0:'First',1:'Second'}, inplace=True)

```

## Select numeric or categorical columns only

To include numeric columns we use

**select_dtypes( )**

```
data1 = iris.select_dtypes(include=[np.number])
data1.head()
```

**_get_numeric_data**

also provides utility to select the numeric columns only.

```
data3 = iris._get_numeric_data()
data3.head(3)
```

```
   Sepal.Length  Sepal.Width  Petal.Length  Petal.Width  cum_sum  cumsum2
0           5.1          3.5           1.4          0.2      5.1      5.1
1           4.9          3.0           1.4          0.2     10.0     10.0
2           4.7          3.2           1.3          0.2     14.7     14.7

```

For selecting categorical variables

```
data4 = iris.select_dtypes(include = ['object'])
data4.head(2)
```

```
 Species
0  setosa
1  setosa

```
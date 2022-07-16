# GroupBy function

To group the data by a categorical variable we use

**groupby( )**

function and hence we can do the operations on each category.

```
income.groupby("Index")["Y2002","Y2003"].min()

```

```
        Y2002    Y2003
Index
A      1170302  1317711
C      1343824  1232844
D      1111437  1268673
F      1964626  1468852
G      1929009  1541565
H      1461570  1200280
I      1353210  1438538
K      1509054  1290700
L      1584734  1110625
M      1221316  1149931
N      1395149  1114500
O      1173918  1334639
P      1320191  1446723
R      1501744  1942942
S      1159037  1150689
T      1520591  1310777
U      1771096  1195861
V      1134317  1163996
W      1677347  1380662

```

To run multiple summary functions, we can use

```
agg( )
```

function which is used to aggregate the data.

```
income.groupby("Index")["Y2002","Y2003"].agg(["min","max","mean"])

```

The following command finds minimum and maximum values for Y2002 and only mean for Y2003

```
income.groupby("Index").agg({"Y2002": ["min","max"],"Y2003" : "mean"})
```

```
          Y2002                 Y2003
           min      max         mean
Index
A      1170302  1742027  1810289.000
C      1343824  1685349  1595708.000
D      1111437  1330403  1631207.000
F      1964626  1964626  1468852.000
G      1929009  1929009  1541565.000
H      1461570  1461570  1200280.000
I      1353210  1776918  1536164.500
K      1509054  1813878  1369773.000
L      1584734  1584734  1110625.000
M      1221316  1983285  1535717.625
N      1395149  1885081  1382499.625
O      1173918  1802132  1569934.000
P      1320191  1320191  1446723.000
R      1501744  1501744  1942942.000
S      1159037  1631522  1477072.000
T      1520591  1811867  1398343.000
U      1771096  1771096  1195861.000
V      1134317  1146902  1498122.500
W      1677347  1977749  1521118.500

```

In order to

```
rename
```

the columns after

```
groupby
```

, you can use tuple. See the code below.

```
income.groupby("Index").agg({"Y2002" : [("Y2002_min","min"),("Y2002_max","max")],
                             "Y2003" : [("Y2003_mean","mean")]})

```

Renaming columns can also be done via the method below.

```
dt = income.groupby("Index").agg({"Y2002": ["min","max"],"Y2003" : "mean"})
dt.columns = ['Y2002_min', 'Y2002_max', 'Y2003_mean']

```

Groupby more than 1 column

```
income.groupby(["Index", "State"]).agg({"Y2002": ["min","max"],"Y2003" : "mean"})

```

By default, option

```
as_index=True
```

is enabled in groupby which means the columns you use in groupby will become an index in the 
new dataframe. To disable it, you can make it False which stores the variables you use in groupby in different columns in the new dataframe.

```
dt = income.groupby(["Index","State"], as_index=False)["Y2002","Y2003"].min()
```

I have the following dataframe describing the percent of shares held by a type of investor in a company:

```
    company  investor   pct
       1       A         1
       1       A         2
       1       B         4
       2       A         2
       2       A         4
       2       A         6
       2       C         10
       2       C         8

```

And I would like to create a new column for each investor type computing the mean of the shares held in each company. I also need to keep the same lenght of the dataset, using transform for instance.

Here is the result I would like to have:

```
     company  investor   pct   pct_mean_A   pct_mean_B   pct_mean_C
       1       A         1        1.5          4            0
       1       A         2        1.5          4            0
       1       B         4        1.5          4            0
       2       A         2        4.0          0            9
       2       A         4        4.0          0            9
       2       A         6        4.0          0            9
       2       C         10       4.0          0            9
       2       C         8        4.0          0            9

```

## 1 Answer

Sorted by:

Use `[groupby](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.groupby.html)` with aggregate `mean` and reshape by `[unstack](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.unstack.html)` for helper `DataFrame` which is `[join](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.join.html)` to original `df`:

```
s = (df.groupby(['company','investor'])['pct']
       .mean()
       .unstack(fill_value=0)
       .add_prefix('pct_mean_'))

df = df.join(s, 'company')
print (df)
   company investor  pct  pct_mean_A  pct_mean_B  pct_mean_C
0        1        A    1         1.5         4.0         0.0
1        1        A    2         1.5         4.0         0.0
2        1        B    4         1.5         4.0         0.0
3        2        A    2         4.0         0.0         9.0
4        2        A    4         4.0         0.0         9.0
5        2        A    6         4.0         0.0         9.0
6        2        C   10         4.0         0.0         9.0
7        2        C    8         4.0         0.0         9.0

```

Or use `[pivot_table](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html)` with default aggregate function `mean`:

```
s = df.pivot_table(index='company',
                   columns='investor',
                   values='pct',
                   fill_value=0).add_prefix('pct_mean_')
df = df.join(s, 'company')
print (df)
   company investor  pct  pct_mean_A  pct_mean_B  pct_mean_C
0        1        A    1         1.5           4           0
1        1        A    2         1.5           4           0
2        1        B    4         1.5           4           0
3        2        A    2         4.0           0           9
4        2        A    4         4.0           0           9
5        2        A    6         4.0           0           9
6        2        C   10         4.0           0           9
7        2        C    8         4.0           0           9

```

**pd.crosstab( )**

is used to create a bivariate frequency distribution. Here the bivariate frequency distribution is between

**Index**

and

**State**

columns.

```
pd.crosstab(income.Index,income.State)
```
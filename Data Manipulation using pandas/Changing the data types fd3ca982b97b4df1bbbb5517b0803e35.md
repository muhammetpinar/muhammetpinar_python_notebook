# Changing the data types

Y2008 is an integer. Suppose we want to convert it to **float** (numeric variable with decimals) we can write:

```
income.Y2008 = income.Y2008.astype(float)
income.dtypes
```

```
Index     object
State     object
Y2002      int64
Y2003      int64
Y2004      int64
Y2005      int64
Y2006      int64
Y2007      int64
Y2008    float64
Y2009      int64
Y2010      int64
Y2011      int64
Y2012      int64
Y2013      int64
Y2014      int64
Y2015      int64
dtype: object
```

To view the dimensions or shape of the data

```
income.shape
```

```
 (51, 16)

```

51 is the number of rows and 16 is the number of columns.

You can also use

**shape[0]**

to see the number of rows (similar to nrow() in R) and

**shape[1]**

for number of columns (similar to ncol() in R).

```
income.shape[0]
income.shape[1]
```

Like factors() function in R, we can include categorical variable in python using **"category"** dtype.

```
s = pd.Series([1,2,3,1,2], dtype="category")
s
```

```
0    1
1    2
2    3
3    1
4    2
dtype: category
Categories (3, int64): [1, 2, 3]

```
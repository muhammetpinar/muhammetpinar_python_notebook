# SQL LIKE Operator in Pandas DataFrame

In SQL, LIKE Statement is used to find out if a character string matches or contains a pattern. We can implement similar functionality in python using

```
str.contains( )
```

function.

```
df2 = pd.DataFrame({"var1": ["AA_2", "B_1", "C_2", "a_2"],
                    "var2": ["X_2", "Y_1", "Z_2", "X2"]})

```

```
   var1 var2
0  AA_2  X_2
1   B_1  Y_1
2   C_2  Z_2
3   a_2   X2

```

How to find rows containing either A or B in variable var1?

```
df2['var1'].str.contains('A|B')
```

```
str.contains(pattern)
```

is used to match pattern in Pandas Dataframe.

```
Output
0     True
1     True
2    False
3    False

```

> The above command returns
> 
> 
> **FALSE**
> 
> ```
> case=False
> ```
> 

```
df2['var1'].str.contains('A|B', case=False)
```

How to filter rows containing a particular pattern?In the following program, we are asking Python to subset data with condition - contain character values either A or B. It is equivalent to WHERE keyword in SQL.

```
df2[df2['var1'].str.contains('A|B', case=False)]
```

```
Output
 var1 var2
0  AA_2  X_2
1   B_1  Y_1
3   a_2   X2

```

Suppose you want only those values that

**have alphabet followed by '_'**

```
df2[df2['var1'].str.contains('^[A-Z]_', case=False)]

```

```
^
```

is a token of regular expression which means begin with a particular item.

```
  var1 var2
1  B_1  Y_1
2  C_2  Z_2
3  a_2   X2

```

## Find position of a particular character or keyword

```
str.find(pattern)
```

is used to find position of sub-string. In this case, sub-string is '_'.

```
df2['var1'].str.find('_')

```

```
0    2
1    1
2    1
3    1

```
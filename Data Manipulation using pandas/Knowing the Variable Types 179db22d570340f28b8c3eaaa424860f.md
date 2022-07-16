# Knowing the Variable Types

You can use the **dataFrameName.dtypes** command to extract the information of types of variables stored in the data frame.

```
income.dtypes
```

```
Index    object
State    object
Y2002     int64
Y2003     int64
Y2004     int64
Y2005     int64
Y2006     int64
Y2007     int64
Y2008     int64
Y2009     int64
Y2010     int64
Y2011     int64
Y2012     int64
Y2013     int64
Y2014     int64
Y2015     int64
dtype: object

```

Here ' **object** ' means strings or character variables. ' **int64** ' refers to numeric variables (without decimals).

To see the variable type of one variable (let's say "State") instead of all the variables, you can use the command below -

```
income['State'].dtypes
```

It returns

**dtype('O').**

In this case, 'O' refers to object i.e. type of variable as a character.
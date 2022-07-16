# Calculating the Cumulative sum

Using

**cumsum( )**

function we can obtain the cumulative sum

```
iris['cum_sum'] = iris["Sepal.Length"].cumsum()
iris.head()
```

Cumulative sum by a variable

To find the cumulative sum of sepal lengths for different species we use

**groupby( )**

and then use

**cumsum( )**

```
iris["cumsum2"] = iris.groupby(["Species"])["Sepal.Length"].cumsum()
iris.head()
```
# Ranking

To create a dataframe of all the ranks we use

**rank( )**

```
iris.rank()
```

Ranking by a specific variable Suppose we want to rank the Sepal.Length for different species in ascending order:

```
iris['Rank2'] = iris['Sepal.Length'].groupby(iris["Species"]).rank(ascending=1)
iris.head()
```
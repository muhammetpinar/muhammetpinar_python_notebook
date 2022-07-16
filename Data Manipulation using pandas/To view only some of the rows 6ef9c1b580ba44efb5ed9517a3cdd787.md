# To view only some of the rows

By default

**head( ) shows first 5 rows**

. If we want to see a specific number of rows we can mention it in the parenthesis. Similarly

**tail( ) function shows last 5 rows by default**.

```
income.head()
income.head(2)  #shows first 2 rows.
income.tail()
income.tail(2)  #shows last 2 rows
```

Alternatively, any of the following commands can be used to fetch first five rows.

```
income[0:5]
```

```
income.iloc[0:5]
```
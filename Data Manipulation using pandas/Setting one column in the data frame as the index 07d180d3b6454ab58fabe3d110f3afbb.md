# Setting one column in the data frame as the index

Using

**set_index("column name")**

we can set the indices as that column and that column gets removed.

```
income.set_index("Index",inplace = True)
income.head()
#Note that the indices have changed and Index column is now no more a column
income.columns
income.reset_index(inplace = True)
income.head()
```

**reset_index( )**

tells us that one should use the by default indices.

Removing columns and rows
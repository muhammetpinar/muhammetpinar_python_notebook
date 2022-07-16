# SQL IN Operator in Pandas

We can use

```
isin(list)
```

function to include multiple values in our filtering or subsetting criteria.

```
mydata = pd.DataFrame({'product': ['A', 'B', 'B', 'C','C','D','A']})
mydata[mydata['product'].isin(['A', 'B'])]

```

```
  product
0       A
1       B
2       B
6       A

```

How to apply NOT criteria while selecting multiple values?

We can use sign

```
~
```

to tell python to negate the condition.

```
mydata[~mydata['product'].isin(['A', 'B'])]

```
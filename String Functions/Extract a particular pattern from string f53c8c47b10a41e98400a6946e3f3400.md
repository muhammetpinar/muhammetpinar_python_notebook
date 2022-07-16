# Extract a particular pattern from string

```
str.extract(r'regex-pattern')
```

is used for this task.

```
df2['var1'].str.extract(r'(^[A-Z]_)')

```

```
r'(^[A-Z]_)'
```

means starts with A-Z and then followed by '_'

```
0    NaN
1     B_
2     C_
3    NaN

```

To remove missing values, we can use

```
dropna( )
```

function.

```
df2['var1'].str.extract(r'(^[A-Z]_)').dropna()

```
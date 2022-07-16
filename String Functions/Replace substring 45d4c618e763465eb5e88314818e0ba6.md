# Replace substring

```
str.replace(old_text,new_text,case=False)
```

is used to replace a particular character(s) or pattern with some new value or pattern. In the code below, we are replacing _ with -- in variable var1.

```
df2['var1'].str.replace('_', '--', case=False)

```

```
Output
0    AA--2
1     B--1
2     C--2
3     A--2

```

We can also complex patterns like the following program.

```
+
```

means item occurs one or more times. In this case, alphabet occurring 1 or more times.

```
df2['var1'].str.replace('[A-Z]+_', 'X', case=False)

```

```
0    X2
1    X1
2    X2
3    X2

```
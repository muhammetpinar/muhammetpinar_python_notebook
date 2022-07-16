# Find length of string

```
len(string)
```

is used to calculate length of string. In pandas data frame, you can apply

```
str.len()
```

for the same.

```
df2['var1'].str.len()

```

```
Output
0    4
1    3
2    3
3    3

```

To find count of occurrence of a particular character (let's say, how many time 'A' appears in each row), you can use

```
str.count(pattern)
```

function.

```
df2['var1'].str.count('A')
```
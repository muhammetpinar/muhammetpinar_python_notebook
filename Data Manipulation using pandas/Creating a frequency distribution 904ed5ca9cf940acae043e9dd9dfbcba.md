# Creating a frequency distribution

**income.Index**

selects the 'Index' column of 'income' dataset and

**value_counts( )**

creates a frequency distribution. By default

**ascending = False**

i.e. it will show the 'Index' having the maximum frequency on the top.

```
income.Index.value_counts(ascending = True)
```

```
F    1
G    1
U    1
L    1
H    1
P    1
R    1
D    2
T    2
S    2
V    2
K    2
O    3
C    3
I    4
W    4
A    4
M    8
N    8
Name: Index, dtype: int64

```
# Lambda Function

## Syntax of Lambda Function

> lambda arguments: expression
> 

Lambda function can have more than one argument but expression cannot be more than 1. The expression is evaluated and returned.

**Example**

```
addition = lambda x,y: x + y
addition(2,3) returns 5

```

In the above python code,

```
x,y
```

are the arguments and

```
x + y
```

is the expression that gets evaluated and returned.

## Difference between Lambda and Def Function

By using both

```
lambda
```

and

```
def
```

, you can create your own user-defined function in python.

`def square(x):
     return x**2
 
square(2) returns 4`

`square = lambda x:x**2

square(2) returns 4`

There are some difference between them as listed below.

1. `lambda`  is a keyword that returns a function object and does not create a 'name'. Whereas `def`  creates name in the local namespace
2. `lambda`  functions are good for situations where you
want to minimize lines of code as you can create function in one line of python code. It is not possible using `def`
3. `lambda`  functions are somewhat less readable for most Python users.
4. `lambda`  functions can only be used once, unless assigned to a variable name.

Lambda functions are used along with built-in functions like filter(), map(), reduce().

## map() function

map functions executes the function object (i.e. lambda or def) for each element and returns a list of the elements modified by the function object. In the code below, we are multiplying each element by 2.

```
mylist = [1, 2, 3, 4]
map(lambda x : x*2, mylist)

```

It returns map object. You cannot see the returned values directly. To view the result, you need to wrap it in

```
list( )
```

```
list(map(lambda x : x*2, mylist))
Output : [2, 4, 6, 8]
```

## filter() function

It returns the items where function is true. If none of the element meets condition, it will return nothing. In the code below, we are checking if value is greater than 2.

```
list(filter(lambda x : x > 2 , mylist))
Output : [3, 4]
```

It returns filter object. To see the output values, you need to put filter( ) function within

```
list( )
```

Let's say you have a dictionary and you want to filter them by values of specific keys.

```
d = {'a': [1, 2, 1], 'b': [3, 4, 1], 'c': [5, 6, 2]}

```

We are filtering values equal to 1 in key 'a' and greater than 1 in key 'b'.

```
list(filter(lambda x: x[0]==1 and x[1]>1, zip(d['a'],d['b'])))

Output

[(1, 3)]

```

Here x[0] refers to d['a'] and x[1] refers to d['b'].

## reduce() function

Syntax of reduce function is as follows :

> reduce(function, list or tuple)
> 

```
from functools import reduce
reduce(lambda x,y: x+y, [1,2,3,4])

```

It returns 10.

How reduce function works?

1. First step, it executes (1 + 2) which returns 3
2. Second step, 3 from first step will be added to 3 (which is third value of the list) and returns 6
3. Third step, 6 from second step will be added to 4 and returns 10

Another example : Reduce function

```
reduce(lambda x,y: x*y, [1,2,3])

```

It evaluates to (1*2)*3 which returns 6.

## Lambda Function : Examples

In this section of tutorial, we will see various practical examples of lambda functions. Let's create a pandas data frame for illustration purpose.

```
import pandas as pd
np.random.seed(12)
df = pd.DataFrame(np.random.randn(5, 3), index=list('abcde'), columns=list('XYZ'))

```

```
          X         Y         Z
a  0.472986 -0.681426  0.242439
b -1.700736  0.753143 -1.534721
c  0.005127 -0.120228 -0.806982
d  2.871819 -0.597823  0.472457
e  1.095956 -1.215169  1.342356

```

Example 1 : Add 2 to each value of Data Frame

```
def add2(x):
     return x+2
df.apply(add2)

```

`df.apply(lambda x: x+2)`

Using

```
apply( )
```

function, you can apply function to pandas dataframe. Both lambda and def returns the same output but

**lambda**

function can be defined inline within apply( ) function.

```
          X         Y         Z
a  2.472986  1.318574  2.242439
b  0.299264  2.753143  0.465279
c  2.005127  1.879772  1.193018
d  4.871819  1.402177  2.472457
e  3.095956  0.784831  3.342356

```

Example 2 : Create function that returns result of number raised to power 

Here we are taking cube of each value of all the variables of df dataframe.

`def power(x,n):
     return x**n 
df.apply(power, n=3)`

`df.apply(lambda x : x**3)`

```
              X         Y         Z
a  1.058143e-01 -0.316414  0.014250
b -4.919381e+00  0.427201 -3.614836
c  1.347751e-07 -0.001738 -0.525523
d  2.368489e+01 -0.213657  0.105460
e  1.316375e+00 -1.794361  2.418820

```

Example 3 : Conditional Statement (IF-ELSE)

Suppose you want to create a new variable which is missing or blank if value of an existing variable is less than 90. Else copy the same value of existing variable. Let's create a dummy data frame called sample which contains only 1 variable named var1. Condition : If var1 is less than 90, function should return missing else value of var1. 

import numpy as np
sample = pd.DataFrame({'var1':[10,100,40] })

```
sample['newvar1'] = sample.apply(lambda x: np.nan if x['var1'] < 90 else x['var1'], axis=1)
```

**How to read the above lambda function**

> x: value_if_condition_true if logical_condition else value_if_condition_false
> 

**axis=1**

tells python to apply function to each row of a particular column. By default, it is 0 which means apply function to each column of a row.

There is one more way to write the above function without specifying axis option. It will be applied to series

**sample['var1']**

```
sample['newvar1'] = sample['var1'].apply(lambda x: np.nan if x < 90 else x)

```

The same function can also be written using def. See the code below.

`def miss(x):
    if x["var1"] < 90:
        return np.nan
    else:
        return x["var1"]

sample['newvar1'] = sample.apply(miss, axis=1)`

```
   var1  newvar1
0    10      NaN
1   100    100.0
2    40      NaN

```

Example 4 : Multiple or Nested IF-ELSE Statement

Suppose you want to create a flag wherein it is yes when value of a variable is greater than or equal to 1 but less than or equal to 5. Else it is no if value is equal to 7. Otherwise missing.

```
mydf = pd.DataFrame({'Names': np.arange(1,10,2)})
mydf["flag"] = mydf["Names"].apply(lambda x: "yes" if x>=1 and x<=5 else "no"
        if x==7 else np.nan)

```

```
   Names flag
0      1  yes
1      3  yes
2      5  yes
3      7   no
4      9  NaN

```
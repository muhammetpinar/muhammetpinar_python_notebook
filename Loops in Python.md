# Loops in Python

## What is Loop?

Loop is an important programming concept and exist in almost every programming language (Python, C, R, Visual Basic etc.). It is used to repeat a particular operation(s) several times until a specific condition is met. It is mainly used to automate repetitive tasks.

## Real World Examples of Loop

1. Software of the ATM machine is in a loop to process transaction after transaction until you acknowledge that you have no more to do.
2. Software program in a mobile device allows user to unlock the mobile with 5 password attempts. After that it resets mobile device.
3. You put your favorite song on a repeat mode. It is also a loop.
4. You want to run a particular analysis on each column of your data set.

## For Loop Python - Syntax and Examples

Like R and C programming language, you can use **for loop** in Python. It is one of the most commonly used loop method to automate the repetitive tasks.

**How for loop works?**

Suppose you are asked to print sequence of numbers from 1 to 9, increment by 2.

```
for i in range(1,10,2):
  print(i)

```

**Output**

```
1
3
5
7
9

```

```
range(1,10,2)
```

means starts from 1 and ends with 9 (excluding 10), increment by 2.

**Iteration over list**

This section covers how to run

**for in loop**

on a list.

```
mylist = [30,21,33,42,53,64,71,86,97,10]
for i in mylist:
    print(i)

```

**Output**

```
30
21
33
42
53
64
71
86
97
10

```

**Suppose you need to select every 3rd value of list.**

```
for i in mylist[::3]:
    print(i)

```

**Output**

```
30
42
71
10

```

```
mylist[::3]
```

is equivalent to

**mylist[0::3]**

which follows this syntax style

```
list[start:stop:step]
```

Python Loop Explained with Examples

---

**Example 1 : Create a new list with only items from list that is between 0 and 10**

```
l1 = [100, 1, 10, 2, 3, 5, 8, 13, 21, 34, 55, 98]

new = [] #Blank list
for i in l1:
    if i > 0 and i <= 10:
        new.append(i)

new

```

```
Output: [1, 10, 2, 3, 5, 8]

```

It can also be done via

**numpy package**

by creating list as numpy array. See the code below.

> import numpy as np
> 

**Example 2 : Check which alphabet (a-z) is mentioned in string**

Suppose you have a string named

**k**

and you want to check which alphabet exists in the string k.

```
k = "deepanshu"

import string
for n in string.ascii_lowercase:
    if n in k:
        print(n + ' exists in ' + k)
    else:
        print(n + ' does not exist in ' + k)

```

```
string.ascii_lowercase
```

returns 'abcdefghijklmnopqrstuvwxyz'.

**Practical Examples : for in loop in Python**

*Create sample pandas data frame for illustrative purpose.*

```
import pandas as pd
np.random.seed(234)
df = pd.DataFrame({"x1" : np.random.randint(low=1, high=100, size=10),
                     "Month1" : np.random.normal(size=10),
                     "Month2" : np.random.normal(size=10),
                     "Month3" : np.random.normal(size=10),
                     "price"  : range(10)
                     })

df

```

**1. Multiple each month column by 1.2**

```
for i in range(1,4):
    print(df["Month"+str(i)]*1.2)

```

> range(1,4) returns 1, 2 and 3.
> 
> 
> ```
> str( ) function is used to covert to string.
> ```
> 

**2. Store computed columns in new data frame**

```
import pandas as pd
newDF = pd.DataFrame()
for i in range(1,4):
    data = pd.DataFrame(df["Month"+str(i)]*1.2)
    newDF=pd.concat([newDF,data], axis=1)

```

> pd.DataFrame( ) is used to create blank data frame.
> 

**3. Check if value of x1 >= 50, multiply each month cost by price. Otherwise same as month.**

```
import pandas as pd
import numpy as np
for i in range(1,4):
    df['newcol'+str(i)] = np.where(df['x1'] >= 50,
                                   df['Month'+str(i)] * df['price'],
                                   df['Month'+str(i)])

```

> In this example, we are adding new columns named
> 
> 
> **newcol1, newcol2 and newcol3.**
> 
> ```
> np.where(condition, value_if condition meets, value_if condition does not meet)
> ```
> 

**4. Filter data frame by each unique value of a column and store it in a separate data frame**

```
mydata = pd.DataFrame({"X1" : ["A","A","B","B","C"]})

for name in mydata.X1.unique():
    temp = pd.DataFrame(mydata[mydata.X1 == name])
    exec('{} = temp'.format(name))

```

> The
> 
> 
> **unique( )**
> 
> **exec( )**
> 
> **See the usage of string format( ) function below -**
> 

```
s= "Your Input"
"i am {}".format(s)

Output: 'i am Your Input'
```

**Loop Control Statements**

Loop control statements change execution from its normal iteration. When execution leaves a scope, all automatic objects that were created in that scope are destroyed.

Python supports the following control statements.

1. Continue statement
2. Break statement

**Continue Statement**

When continue statement is executed, it skips the further code in the loop and continue iteration.

In the code below, we are avoiding letters a and d to be printed.

```
for n in "abcdef":
    if n =="a" or n =="d":
       continue
    print("letter :", n)

```

```
letter : b
letter : c
letter : e
letter : f

```

**Break Statement**

When break statement runs, it breaks or stops the loop.

In this program, when n is either c or d, loop stops executing.

```
for n in "abcdef":
    if n =="c" or n =="d":
       break
    print("letter :", n)

```

```
letter : a
letter : b

```

## for loop with else clause

Using

**else clause**

with

**for loop**

is not common among python developers community.

> The
> 
> 
> **else clause**
> 

The program below calculates factors for numbers between 2 to 10. Else clause returns numbers which have no factors and are therefore prime numbers:

```
for k in range(2, 10):
    for y in range(2, k):
        if k % y == 0:
            print( k, '=', y, '*', round(k/y))
            break
    else:
        print(k, 'is a prime number')

```

```
2 is a prime number
3 is a prime number
4 = 2 * 2
5 is a prime number
6 = 2 * 3
7 is a prime number
8 = 2 * 4
9 = 3 * 3

```

## While Loop

While loop is used to execute code repeatedly until a condition is met. And when the condition becomes false, the line immediately after the loop in program is executed.

```
i = 1
while i < 10:
    print(i)
    i += 2 #means i = i + 2
    print("new i :", i)

```

```
Output:
1
new i : 3
3
new i : 5
5
new i : 7
7
new i : 9
9
new i : 11

```

**While Loop with If-Else Statement**

If-Else statement can be used along with While loop. See the program below -

```
counter = 1
while (counter <= 5):
    if counter < 2:
        print("Less than 2")
    elif counter > 4:
        print("Greater than 4")
    else:
        print(">= 2 and <=4")
    counter += 1

```
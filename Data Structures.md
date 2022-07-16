# Data Structures

# 1.STRING

Python String is a sequence of characters.

## How to create a string in Python

You can create a Python string using a **single or double quote**

.

```
mystring = "Hello Python3.6"
print(mystring)
```

**Output:**

```
Hello Python3.6

```

### Can I use multiple single or double quotes to define string?

Answer is Yes. See examples below -

Multiple Single Quotes

```
mystring = '''Hello Python3.6'''
print(mystring)
```

**Output:**

```
Hello Python3.6

```

### Multiple Double Quotes

```
mystring = """Hello Python3.6"""
print(mystring)
```

**Output:**

```
Hello Python3.6

```

### How to include quotes within a string?

```
mystring = r'Hello"Python"'
print(mystring)
```

**Output:**

```
Hello"Python"

```

How to extract Nth letter or word?

You can use the syntax below to get first letter.

```
mystring = 'Hi How are you?'
mystring[0]
```

**Output**

```
'H'
```

**mystring[0]**

refers to first letter as indexing in python starts from 0. Similarly, mystring[1] refers to the second letter. To pull the last letter, you can use -1 as an index.

```
mystring[-1]
```

### To get first word

```
mystring.split(' ')[0]
```

**Output :** Hi

How it works -

1. mystring.split(' ') tells Python to use space as a delimiter.

**Output :**

['Hi', 'How', 'are', 'you?']

2. mystring.split(' ')[0] tells Python to pick first word of a string.

# 2.LIST

Unlike String,

**List c**an contain different types of objects such as integer, float, string etc.

1. x = [142, 124, 234, 345, 465]
2. y = [‘A’, ‘C’, ‘E’, ‘M’]
3. z = [‘AA’, 44, 5.1, ‘KK’]

### Get List Item

We can extract list item using Indexes.

**Index starts from 0 and end with (number of elements-1).**

```
Syntax : list[start : stop : step]
```

1. **start :** refers to starting position.
2. **stop :** refers to end position.
3. **step :** refers to increment value.

```
k = [124, 225, 305, 246, 259]
k[0]
k[1]
k[-1]
```

```
k[0]
124

k[1]
225

k[-1]
259

```

Explanation :

```
k[0] picks first element from list. Negative sign tells Python to search list item from right to left. k[-1] selects the last element from list.
```

To select multiple elements from a list, you can use the following method :

```
k[:3] returns [124, 225, 305]
k[0:3] also returns [124, 225, 305]
k[::-1] reverses the whole list and returns [259, 246, 305, 225, 124]

```

Sort list

```
sorted(list)
```

function arranges list in ascending order.

```
sorted(list, reverse=True)
```

function sorts list in descending order.

```
sorted(k) returns [124, 225, 246, 259, 305]
sorted(k, reverse=True) returns [305, 259, 246, 225, 124]

```

Add 5 to each element of a list In the program below, len() function is used to count the number of 
elements in a list. In this case, it returns 5. With the help of range() function, r**ange(5) returns 0,1,2,3,4.**

```
x = [1, 2, 3, 4, 5]
for i in range(len(x)):
    x[i] = x[i] + 5
print(x)
```

```
[6, 7, 8, 9, 10]

```

It can also be written like this -

```
for i in range(len(x)):
   x[i]+= 5
print(x)
```

### Combine / Join two lists The '+' operator is concatenating two lists.

```
X = [1, 2, 3]
Y = [4, 5, 6]
Z = X + Y
print(Z)
```

```
[1, 2, 3, 4, 5, 6]

```

Sum of values of two list

```
X = [1, 2, 3]
Y = [4, 5, 6]
import numpy as np
Z =np.add(X, Y)
print(Z)
```

```
print(Z)
[5 7 9]
```

Similarly, you can use **np.multiply(X, Y)** to multiply values of two list.

Repeat List N times The '*' operator is repeating list N times.

```
X = [1, 2, 3]
Z = X * 3
print(Z)
```

```
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

**Note :** The above two methods also work for **string list**.

Modify / Replace a list item

Suppose you need to replace third value to a different value.

```
X = [1, 2, 3]
X[2]=5
print(X)
```

```
print(X)
[1, 2, 5]

```

Add / Remove a list item We can add a list item by using **append method**

.

```
X = ['AA', 'BB', 'CC']
X.append('DD')
print(X)
```

**Result :**

['AA', 'BB', 'CC', 'DD']

Similarly, we can remove a list item by using **remove method**

.

```
X = ['AA', 'BB', 'CC']
X.remove('BB')
print(X)
```

**Result :**

['AA', 'CC']

# 3. Tuple

Like list, tuple can also contain mixed data. But tuple cannot be mutable or changed once created whereas list can be mutable or modified.

Another difference is a tuple is created inside parentheses **( )**. Whereas, list is created inside square brackets **[ ]**

Examples

```
mytuple = (123,223,323)
City = ('Delhi','Mumbai','Bangalore')
```

### Perform for loop on Tuple

```
for i in City:
    print(i)
```

```
Delhi
Mumbai
Bangalore

```

Tuple cannot be altered. Run the following command and check error

```
X = (1, 2, 3)
X[2]=5
```

TypeError:

'tuple' object does not support item assignment

# 4. Dictionary

It works like an address book where you can find an address of a person by searching the name. In this example. name of a person is considered as **key** and address as **value**. It is important to note that the key must be unique while values may not be. Keys should not be duplicated because if it is a duplicate, you cannot find exact values associated with the key. Keys can be of any data type such as strings, numbers, or tuples.

### Create a dictionary

It is defined in curly braces {}. Each key is followed by a colon (:) and then values.

```
teams = {'Dave' : ['teamA','teamAA', 'teamAB'],
         'Tim'  : ['teamB','teamBB','teamBC'],
         'Babita' : ['teamC','teamCB','teamCC']
        }

```

### Extract Keys and Values of Dictionary

```
teams.keys()
```

returns dict_keys(['Dave', 'Tim', 'Babita'])

```
teams.values()
```

returns dict_values([['teamA', 'teamAA', 'teamAB'], ['teamB', 'teamBB', 'teamBC'], ['teamC', 'teamCB', 'teamCC']])

### Find Values of a particular key

```
teams['Dave']
```

```
Output
['teamA', 'teamAA', 'teamAB']

```

### Delete an item

In the code below, we are removing 'Babita' from teams dict.

```
del teams['Babita']
```

```
Output
{'Dave': ['teamA', 'teamAA', 'teamAB'],
'Tim': ['teamB', 'teamBB', 'teamBC']}

```

### Add an item

Here we are adding one more key named 'Deep' and value against it is 'team D'.

```
teams['Deep'] = 'team D'
```

```
Output
{'Dave': ['teamA', 'teamAA', 'teamAB'],
 'Deep': 'team D',
 'Tim': ['teamB', 'teamBB', 'teamBC']}

```

You can also create dictionary like the way it is shown below

```
d={}
d['a'] = 1
d['b'] = 2
print(d)
{'a': 1, 'b': 2}

```

### How to create a dictionary from lists

Suppose you have keys and values stored in two separate lists. You can use and zip them to create a dictionary.

```
keys = ['a', 'b', 'c']
values = [1, 2, 3]
d1 = dict(zip(keys, values))

```

# 5. Sets

Sets are unordered collections of simple objects. They are mainly used to check whether an object is present in the set and compute mathematical operations such as intersection, union, difference etc.

```
X = set(['A', 'B', 'C'])
```

Q. Does 'A' exist in set X?

```
'A' in X
```

**Result :**

True

Q. Does 'D' exist in set X?

```
'D' in X
```

**Result :**

False

Q. How to add 'D' in set X?

```
X.add('D')
```

Q. How to remove 'C' from set X?

```
X.remove('C')
```

Q. How to create a copy of set X?

```
Y = X.copy()
```

Q. Which items are common in both sets X and Y?

```
Y & X
```

Practical Examples: Python Data Structures

The examples below would help you to understand what kind of operations on data structures are commonly used in the real-world.

1. How to find intersection and union of two lists

```
x = [1, 2, 3, 4]
y = [2, 3, 6, 5]

list(set(x) & set(y))
list(set(x) | set(y))

```

```
&
```

the symbol refers to 'and' condition which means common between two lists.

```
|
```

the symbol refers to 'or' condition.

2. Check whether an item exists in the list

```
x = [1, 2, 3, 4]
3 in x

True
```

3. Check whether multiple items exist in the list

all returns are True only when all the items exist. any returns when any of the items exist.

```
all(i in x for i in [1,6])
False

any(i in x for i in [1,6])
True
```
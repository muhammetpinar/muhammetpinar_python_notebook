# Python Dictionary Comprehension

What is Dictionary?

Dictionary is a data structure in python which is used to store data such that values are connected to their related key. Roughly it works very similar to SQL tables or data stored in statistical oftwares. It has two main components -

1. Keys : Think about columns in tables. It must be unique (like column names cannot be duplicate)
2. Values : It is similar to rows in tables. It can be duplicate.

It is defined in curly braces { }. Each key is followed by a colon (:) and then values.

Syntax of Dictionary

```
d = {'a': [1,2], 'b': [3,4], 'c': [5,6]}

```

To extract keys, values and structure of dictionary, you can submit the following commands.

```
d.keys() # 'a', 'b', 'c'
d.values() # [1, 2], [3, 4], [5, 6]
d.items()

```

Like R or SAS, you can create dataframe or dataset using

[pandas](https://www.listendata.com/2017/12/python-pandas-tutorial.html)

package in python.

```
import pandas as pd
pd.DataFrame(data=d)

```

```
   a  b  c
0  1  3  5
1  2  4  6

```

## What is Dictionary Comprehension?

Like

[List Comprehension](https://www.listendata.com/2019/07/python-list-comprehension-with-examples.html)

, Dictionary Comprehension lets us to run

```
for loop
```

on dictionary with a single line of code.

Both list and dictionary comprehension are a part of functional programming which aims to make coding more readable and create list and dictionary in a crisp way without explicitly using for loop.

The difference between list and dictionary comprehension is that list comprehension creates list. Whereas dictionary comprehension creates dictionary. Syntax is also slightly different (refer the succeeding section). List is defined with square bracket

```
[ ]
```

whereas dictionary is created with

```
{ }
```

## Syntax of Dictionary Comprehension

> {key: value for (key, value) in iterable}
> 

**Iterable**

is any python object in which you can loop over. For example, list, tuple or string.

```
keys = ['a', 'b', 'c']
values = [1, 2, 3]
{i:j for (i,j) in zip(keys, values)}

```

It creates dictionary

```
{'a': 1, 'b': 2, 'c': 3}
```

. It can also be written without dictionary comprehension like

```
dict(zip(keys, values))
```

.

You can also execute dictionary comprehension with just defining only one variable `i`. In the example below, we are taking square of i for assigning values in dictionary.

`range(5)` returns 0 through 4 as indexing in python starts from 0 and excluding end point. If you want to know how dictionary comprehension is different from For Loop, refer the table below.

**Dictionary Comprehension**

`d = {i:i**2 for i in range(5)}`

**For Loop**

`d = {}
for i in range(5):
    d[i]=i**2
print(d)`

```
Output
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

```

```
d.keys() returns [0, 1, 2, 3, 4]
d.values() returns [0, 1, 4, 9, 16]

```

## Create dictionary containing alphabets as keys

Suppose you want letters from 'a' through 'e' as keys in dictionary and digits from 0 through 4 as values.

```
string.ascii_lowercase[:5]
```

returns abcde.

```
import string
{i:j for (i, j) in zip(string.ascii_lowercase[:5], range(5))}

```

```
{'a': 0, 'b': 1, 'c': 2, 'd': 3, 'e': 4}

```

## Create new dictionary out of existing dictionary

```
dic.items()
```

returns the whole structure of dictionary which comprises of both keys and values. In the following example, we are multiplying values of existing dictionary by 2 and building a new dictionary named new_dic.

```
dic = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
new_dic = {i:j*2 for i,j in dic.items()}
new_dic

```

```
{'a': 2, 'b': 4, 'c': 6, 'd': 8}

```

## How to use IF statement in Dictionary Comprehension

Here we are applying conditional statement and considering values above 2.

```
dic = {'a': 1, 'b': 2, 'c': 3, 'd': 4}
{i:j*2 for (i,j) in dic.items() if j>2}

```

```
Output
{'c': 6, 'd': 8}

```

## IF-ELSE condition in Dictionary Comprehension

You can apply if-else statement like we do in list comprehension. This example outlines how to show odd or even numbers in values in dictionary.

```
{i:('even' if j%2==0 else 'odd') for (i,j) in dic.items()}

```

```
{'a': 'odd', 'b': 'even', 'c': 'odd', 'd': 'even'}
```

## Use Enumerate Function in dictionary comprehension

Enumerate function runs on list, tuple or string and returns element and its index.

```
list(enumerate(['a', 'b', 'c']))
```

```
Output
[(0, 'a'), (1, 'b'), (2, 'c')]

```

With the use of this function, we can create a dictionary with elements of the list as keys and the index as values.

```
mylist = ['a', 'b', 'c']
{j:i for i,j in enumerate(mylist)}

```

```
{'a': 0, 'b': 1, 'c': 2}

```

## Remove selected items from dictionary

Suppose you have a dictionary containing cities name along with some values and you want to delete specific multiple items (let's say Delhi and London) from dictionary. In this example, i refers to keys of dictionary and d[i] evaluates to d[key]. For e.g.

**d['Mumbai] returns 221.**

```
d = {'Delhi': 121, 'Mumbai': 221, 'New York': 302, 'London': 250}
{i:d[i] for i in d.keys() - {'Delhi','London'}}

```

It returns these two items

```
{'Mumbai': 221, 'New York': 302}
```
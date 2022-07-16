# LEFT, RIGHT and MID Functions

If you are intermediate MS Excel users, you must have used LEFT, RIGHT and MID Functions. These functions are used to extract N number of characters or letters from string.

1. Extract first two characters from beginning of stringmystring = "Hey buddy, wassup?"
mystring[:2]

```
Out[1]: 'He'

```

1. `string[start:stop:step]` means item start from 0 (default) through (stop-1), step by 1 (default).
2. `mystring[:2]`  is equivalent to  `mystring[0:2]`
3. `mystring[:2]`  tells Python to pull first 2 characters from `mystring` string object.
4. Indexing starts from zero so it includes first, second element and excluding third.

2. Find last two characters of string

```
mystring[-2:]

```

The above command returns

```
p?
```

.The

- 2

starts the range from second last position through maximum length of string.

3. Find characters from middle of string

```
mystring[1:3]

```

```
Out[1]: 'ey'

```

```
mystring[1:3]
```

returns second and third characters.

**1**

refers to second character as index begins with 0.

4. How to reverse string?

```
mystring[::-1]

```

```
Out[1]: '?pussaw ,yddub yeH'

```

- 1

tells Python to start it from end and increment it by 1 from right to left.

5. How to extract characters from string variable in Pandas DataFrame?

Let's create a fake data frame for illustration. In the code below, we are creating a dataframe named

```
df
```

containing only 1 variable called

```
var1
```

```
import pandas as pd
df = pd.DataFrame({"var1": ["A_2", "B_1", "C_2", "A_2"]})

  var1
0  A_2
1  B_1
2  C_2
3  A_2

```

To deal text data in Python Pandas Dataframe, we can use

```
str
```

attribute. It can be used for slicing character values.

```
df['var1'].str[0]
```

In this case, we are fetching first character from

```
var1
```

variable. See the output shown below.

```
Output
0    A
1    B
2    C
3    A

```
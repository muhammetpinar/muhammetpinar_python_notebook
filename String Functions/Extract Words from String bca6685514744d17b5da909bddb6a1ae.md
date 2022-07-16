# Extract Words from String

Suppose you need to take out word(s) instead of characters from string. Generally we consider one blank space as delimiter to find words from string.

1. Find first word of string

```
mystring.split()[0]

```

```
Out[1]: 'Hey'

```

How it works?

1. `split()` function breaks string using space as a default separator
2. `mystring.split()` returns  `['Hey', 'buddy,', 'wassup?']`
3. `0` returns first item or word  `Hey`

2. Comma as separator for words

```
mystring.split(',')[0]

```

```
Out[1]: 'Hey buddy'

```

3. How to extract last word

```
mystring.split()[-1]

```

```
Out[1]: 'wassup?'
```

4. How to extract word in DataFrame

Let's build a dummy data frame consisting of customer names and call it variable

```
custname
```

```
mydf = pd.DataFrame({"custname": ["Priya_Sehgal", "David_Stevart", "Kasia_Woja", "Sandy_Dave"]})

```

```
        custname
0   Priya_Sehgal
1  David_Stevart
2     Kasia_Woja
3     Sandy_Dave

```

```
#First Word
mydf['fname'] = mydf['custname'].str.split('_').str[0]

#Last Word
mydf['lname'] = mydf['custname'].str.split('_').str[1]

```

Detailed Explanation

1. `str.split( )` is similar to `split( )`. It is used to activate split function in pandas data frame in Python.
2. In the code above, we created two new columns named `fname` and `lname` storing first and last name.

```
Output
        custname  fname    lname
0   Priya_Sehgal  Priya   Sehgal
1  David_Stevart  David  Stevart
2     Kasia_Woja  Kasia     Woja
3     Sandy_Dave  Sandy     Dave

```
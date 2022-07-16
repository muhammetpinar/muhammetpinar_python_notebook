# Concatenate or Join Strings

By simply using

```
+
```

, you can join two string values.

```
x = "Deepanshu"
y ="Bhalla"
x+y

```

```
DeepanshuBhalla

```

In case you want to add a space between two strings, you can use this -

```
x+' '+y
```

returns

```
Deepanshu Bhalla
```

Suppose you have a list containing multiple string values and you want to combine them. You can use

**join( )**

function.

```
string0 = ['Ram', 'Kumar', 'Singh']
' '.join(string0)

```

```
Output
'Ram Kumar Singh'

```

Suppose you want to combine or concatenate two columns of pandas dataframe.

> mydf['fullname'] = mydf['fname'] + ' ' + mydf['lname']
> 

**OR**

> mydf['fullname'] = mydf[['fname', 'lname']].apply(lambda x: ' '.join(x), axis=1)
> 

```
     custname  fname    lname       fullname
0   Priya_Sehgal  Priya   Sehgal   Priya Sehgal
1  David_Stevart  David  Stevart  David Stevart
2     Kasia_Woja  Kasia     Woja     Kasia Woja
3     Sandy_Dave  Sandy     Dave     Sandy Dave

```
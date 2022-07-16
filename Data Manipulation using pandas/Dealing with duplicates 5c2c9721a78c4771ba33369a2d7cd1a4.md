# Dealing with duplicates

We create a new dataframe comprising of items and their respective prices.

```
data = pd.DataFrame({"Items" : ["TV","Washing Machine","Mobile","TV","TV","Washing Machine"], "Price" : [10000,50000,20000,10000,10000,40000]})
data
```

```
             Items  Price
0               TV  10000
1  Washing Machine  50000
2           Mobile  20000
3               TV  10000
4               TV  10000
5  Washing Machine  40000

```

**duplicated()**

returns a logical vector returning True when encounters duplicated.

```
data.loc[data.duplicated(),:]
data.loc[data.duplicated(keep = "first"),:]
```

By default

**keep = 'first'**

i.e. the first occurence is considered a unique value and its repetitions are considered as duplicates.

If

**keep = "last"**

the last occurence is considered a unique value and all its repetitions are considered as duplicates.

```
data.loc[data.duplicated(keep = "last"),:] #last entries are not there,indices have changed.
```

If

**keep = "False"**

then it considers all the occurences of the repeated observations as duplicates.

```
data.loc[data.duplicated(keep = False),:]  #all the duplicates, including unique are shown.
```

To drop the duplicates

**drop_duplicates**

is used with default

**inplace = False,**

keep = 'first' or 'last' or 'False' have the respective meanings as in duplicated( )

```
data.drop_duplicates(keep = "first")
data.drop_duplicates(keep = "last")
data.drop_duplicates(keep = False,inplace = True)  #by default inplace = False
data
```
# Sorting Data

To sort the data

**sort_values( )**

function is deployed. By default

**inplace = False**

and

**ascending = True.**

```
income.sort_values("State",ascending = False)
income.sort_values("State",ascending = False,inplace = True)
income.Y2006.sort_values()
```

We have got duplicated for Index thus we need to sort the dataframe 
firstly by Index and then for each particular index we sort the values 
by Y2002

```
income.sort_values(["Index","Y2002"])
```
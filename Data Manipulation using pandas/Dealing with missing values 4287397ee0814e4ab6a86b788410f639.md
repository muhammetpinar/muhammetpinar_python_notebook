# Dealing with missing values

We create a new dataframe named 'crops' and to create a NaN value we use

**np.nan**

by importing

**numpy**

.

```
import numpy as np
mydata = {'Crop': ['Rice', 'Wheat', 'Barley', 'Maize'],
        'Yield': [1010, 1025.2, 1404.2, 1251.7],
        'cost' : [102, np.nan, 20, 68]}
crops = pd.DataFrame(mydata)
crops
```

**isnull( )**

returns True and

**notnull( )**

returns False if the value is NaN.

```
crops.isnull()  #same as is.na in R
crops.notnull()  #opposite of previous command.
crops.isnull().sum()  #No. of missing values.
```

crops.cost.isnull() firstly subsets the 'cost' from the dataframe and returns a logical vector with isnull()

```
crops[crops.cost.isnull()] #shows the rows with NAs.
crops[crops.cost.isnull()].Crop #shows the rows with NAs in crops.Crop
crops[crops.cost.notnull()].Crop #shows the rows without NAs in crops.Crop
```

To drop all the rows which have missing values in any rows we use

**dropna(how = "any")**

. By default

**inplace = False**

. If

**how = "all"**

means drop a row if all the elements in that row are missing

```
crops.dropna(how = "any").shape
crops.dropna(how = "all").shape
```

To remove NaNs if any of 'Yield' or'cost' are missing we use the subset parameter and pass a list:

```
crops.dropna(subset = ['Yield',"cost"],how = 'any').shape
crops.dropna(subset = ['Yield',"cost"],how = 'all').shape
```

Replacing the missing values by "UNKNOWN" sub attribute in Column name.

```
crops['cost'].fillna(value = "UNKNOWN",inplace = True)
crops
```
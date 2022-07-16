# Finding Descriptive Statistics

**describe( )**

is used to find some statistics like mean,minimum, quartiles etc.

**for numeric variables.**

```
income.describe() #for numeric variables
```

```
              Y2002         Y2003         Y2004         Y2005         Y2006  \
count  5.100000e+01  5.100000e+01  5.100000e+01  5.100000e+01  5.100000e+01
mean   1.566034e+06  1.509193e+06  1.540555e+06  1.522064e+06  1.530969e+06
std    2.464425e+05  2.641092e+05  2.813872e+05  2.671748e+05  2.505603e+05
min    1.111437e+06  1.110625e+06  1.118631e+06  1.122030e+06  1.102568e+06
25%    1.374180e+06  1.292390e+06  1.268292e+06  1.267340e+06  1.337236e+06
50%    1.584734e+06  1.485909e+06  1.522230e+06  1.480280e+06  1.531641e+06
75%    1.776054e+06  1.686698e+06  1.808109e+06  1.778170e+06  1.732259e+06
max    1.983285e+06  1.994927e+06  1.979395e+06  1.990062e+06  1.985692e+06
              Y2007         Y2008         Y2009         Y2010         Y2011  \
count  5.100000e+01  5.100000e+01  5.100000e+01  5.100000e+01  5.100000e+01
mean   1.553219e+06  1.538398e+06  1.658519e+06  1.504108e+06  1.574968e+06
std    2.539575e+05  2.958132e+05  2.361854e+05  2.400771e+05  2.657216e+05
min    1.109382e+06  1.112765e+06  1.116168e+06  1.103794e+06  1.116203e+06
25%    1.322419e+06  1.254244e+06  1.553958e+06  1.328439e+06  1.371730e+06
50%    1.563062e+06  1.545621e+06  1.658551e+06  1.498662e+06  1.575533e+06
75%    1.780589e+06  1.779538e+06  1.857746e+06  1.639186e+06  1.807766e+06
max    1.983568e+06  1.990431e+06  1.993136e+06  1.999102e+06  1.992996e+06
              Y2012         Y2013         Y2014         Y2015
count  5.100000e+01  5.100000e+01  5.100000e+01  5.100000e+01
mean   1.591135e+06  1.530078e+06  1.583360e+06  1.588297e+06
std    2.837675e+05  2.827299e+05  2.601554e+05  2.743807e+05
min    1.108281e+06  1.100990e+06  1.110394e+06  1.110655e+06
25%    1.360654e+06  1.285738e+06  1.385703e+06  1.372523e+06
50%    1.643855e+06  1.531212e+06  1.580394e+06  1.627508e+06
75%    1.866322e+06  1.725377e+06  1.791594e+06  1.848316e+06
max    1.988270e+06  1.994022e+06  1.990412e+06  1.996005e+06

```

**For character or string variables**

, you can write

**include = ['object']**

. It will return total count, maximum occurring string and its frequency

```
income.describe(include = ['object'])  #Only for strings / objects
```

**To find out specific descriptive statistics of each column of data frame**

```
income.mean()
income.median()
income.agg(["mean","median"])
```

```
agg( )
```

performs aggregation with summary functions like sum, mean, median, min, max etc.

**How to run functions for a particular column(s)?**

```
income.Y2008.mean()
income.Y2008.median()
income.Y2008.min()
income.loc[:,["Y2002","Y2008"]].max()
```
# Create new variables

Using

**eval( )**

arithmetic operations on various columns can be carried out in a dataset.

```
income["difference"] = income.Y2008-income.Y2009

#Alternatively
income["difference2"] = income.eval("Y2008 - Y2009")
income.head()
```

```
  Index       State    Y2002    Y2003    Y2004    Y2005    Y2006    Y2007  \
0     A     Alabama  1296530  1317711  1118631  1492583  1107408  1440134
1     A      Alaska  1170302  1960378  1818085  1447852  1861639  1465841
2     A     Arizona  1742027  1968140  1377583  1782199  1102568  1109382
3     A    Arkansas  1485531  1994927  1119299  1947979  1669191  1801213
4     C  California  1685349  1675807  1889570  1480280  1735069  1812546
       Y2008    Y2009    Y2010    Y2011    Y2012    Y2013    Y2014    Y2015  \
0  1945229.0  1944173  1237582  1440756  1186741  1852841  1558906  1916661
1  1551826.0  1436541  1629616  1230866  1512804  1985302  1580394  1979143
2  1752886.0  1554330  1300521  1130709  1907284  1363279  1525866  1647724
3  1188104.0  1628980  1669295  1928238  1216675  1591896  1360959  1329341
4  1487315.0  1663809  1624509  1639670  1921845  1156536  1388461  1644607
   difference  difference2
0      1056.0       1056.0
1    115285.0     115285.0
2    198556.0     198556.0
3   -440876.0    -440876.0
4   -176494.0    -176494.0

```

```
income.ratio = income.Y2008/income.Y2009
```

The above command does not work, thus to create new columns we need to use square brackets.

We can also use

**assign( )**

function but this command does not make changes in the original data as there is no inplace parameter. Hence we need to save it in a new dataset.

```
data = income.assign(ratio = (income.Y2008 / income.Y2009))
data.head()
```
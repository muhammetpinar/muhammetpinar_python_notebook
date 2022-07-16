# Conditions in python

We create a new dataframe of students' name and their respective zodiac signs.

```
students = pd.DataFrame({'Names': ['John','Mary','Henry','Augustus','Kenny'],
                         'Zodiac Signs': ['Aquarius','Libra','Gemini','Pisces','Virgo']})
```

```
def name(row):
    if row["Names"] in ["John","Henry"]:
        return "yes"
    else:
        return "no"
students['flag'] = students.apply(name, axis=1)
students

```

Functions in python are defined using the block keyword

```
def
```

, followed with the function's name as the block's name.

[**apply( )** (1)](Conditions%20in%20python%2076528772b58b4d3eb2a2a28af365d977/apply(%20)%20(1)%201dc4fb197d8c45deb4cc45b05057e95a.md)

function applies function along rows or columns of dataframe.

```
Note :
```

If using simple 'if else'

**we need to take care of the indentation**

. Python does not involve curly braces for the loops and if else.

Output

```
      Names Zodiac Signs flag
0      John     Aquarius  yes
1      Mary        Libra   no
2     Henry       Gemini  yes
3  Augustus       Pisces   no
4     Kenny        Virgo   no

```

**Alternatively**

, By importing numpy we can use

**np.where**

. The first argument is the condition to be evaluated, 2nd argument is the value if condition is True and last argument defines the value if the condition evaluated returns False.

```
import numpy as np
students['flag'] = np.where(students['Names'].isin(['John','Henry']), 'yes', 'no')
students
```

Multiple Conditions : If Else-if Else

```
def mname(row):
    if row["Names"] == "John" and row["Zodiac Signs"] == "Aquarius" :
        return "yellow"
    elif row["Names"] == "Mary" and row["Zodiac Signs"] == "Libra" :
        return "blue"
    elif row["Zodiac Signs"] == "Pisces" :
        return "blue"
    else:
        return "black"
students['color'] = students.apply(mname, axis=1)
students

```

We create a list of conditions and their respective values if evaluated True and use

**np.select**

where default value is the value if all the conditions is False

```
conditions = [
    (students['Names'] == 'John') & (students['Zodiac Signs'] == 'Aquarius'),
    (students['Names'] == 'Mary') & (students['Zodiac Signs'] == 'Libra'),
    (students['Zodiac Signs'] == 'Pisces')]
choices = ['yellow', 'blue', 'purple']
students['color'] = np.select(conditions, choices, default='black')
students
```

```
      Names Zodiac Signs flag   color
0      John     Aquarius  yes  yellow
1      Mary        Libra   no    blue
2     Henry       Gemini  yes   black
3  Augustus       Pisces   no  purple
4     Kenny        Virgo   no   black

```
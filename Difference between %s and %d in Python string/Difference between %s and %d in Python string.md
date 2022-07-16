# Difference between %s and %d in Python string

In this article, we will see the difference between %s and %d in Python. Here, we start with the proper explanation of one at a time, then both, and at last compare these.

## **%s operator**

The % symbol is used in Python with a large variety of data types and configurations. It is used as an argument specifier and string formatter. %s specifically is used to perform concatenation of strings 
together. It allows us to format a value inside a string. It is used to incorporate another string within a string. It automatically provides type conversion from value to string.

The %s operator is put where the string is to be specified. The number of values you want to append to a string should be equivalent to the number specified in parentheses after the % operator at the end of the string value. Following code illustrates the usage of %s symbol :

```sql
# declaring a string variable
name ="Geek"

#append a string within a string

print("Hey, %s!"%name)
```

**Output**

```
Hey, Geek!
```

## **%d operator**

The %d operator is used as a placeholder to specify integer values, decimals or numbers. It allows us to print numbers within strings or other values. The %d operator is put where the integer is to be 
specified. Floating-point numbers are converted automatically to decimal  values.

```sql
#declaring numeric variables
num =2021
#concatenating numeric value within string
print("%d is here!!"% num)
```

**Output**

```
2021 is here!!
```

The  decimal and rational numbers are rounded off to the absolute integral part and the numbers after the decimal are scraped off, that is only the  integers are extracted. The following code illustrates the usage of %d with decimal and fractional numbers:

```sql
#declaring rational number
frac_num = 8/3

#concatenating numeric value within string

print("Rational number formatting using %d")

print("%d is equal to 8/3 using this operator."%frac_num)
#declaring decimal number
dec_num =10.9785
#concatenating numeric value within string
print("Decimal number formatting using %d")
print("%d is equal to 10.9785 using this operator."%dec_num)
```

**Output**

```
Rational number formatting using %d
2 is equal to 8/3 using this operator.
Decimal number formatting using %d
10 is equal to 10.9785 using this operator.
```

## Both %s and %d operators

We  can use a combination of operators also within a single program. Before  that first, clear some concepts by comparing as given below :

[Untitled](Difference%20between%20%25s%20and%20%25d%20in%20Python%20string%20ec51a8bacdff46fa9b356570de7e2cf1/Untitled%20Database%20307d9f2a60804d259ad6525f5a7b96c9.csv)

```sql
name = "Sita"
age =2
print("Using %s and %d both")
print("%s's age is %d."%(name,age))
```

**Output**

```
Using %s and %d both
Sita's age is 22.
```

**Note 1:** %s automatically converts numeric value to a string without throwing an error.

```sql
name = "Sita"
age = 22
print("Using %s ")
print ("%s's age is %s."%(name,age))
```

**Output**

```
Using %s
Sita's age is 22.
```

**Note 2:** %d, however, can only be used for numeric values. Otherwise, an error is returned.

```sql
name = "Sita"
age = 22
print("Using %d")
print ("%d's age is %d."%(name,age))
```

**Error**

```
Using %d
Traceback (most recent call last):
 File "<string>", line 4, in <module>
TypeError: %d format: a number is required, not str
```
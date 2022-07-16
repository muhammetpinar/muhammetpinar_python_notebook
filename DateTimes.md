# DateTimes

## Introduction : datetime module

It is a python module which provides several functions for dealing with dates and time. It has four classes as follows which are explained in the latter part of this article how these classes work.

1. datetime
2. date
3. time
4. timedelta

People who have no experience of working with real-world datasets might have not encountered date columns. They might be under impression that working with dates is rarely used and not so important. To enlighten them, I have listed down real-world examples wherein using datetime module can be beneficial.

1. Selecting all the saving account holders who were active on 30th June, 2018 and checking their status whether they are still active
2. Identifying insureds who filed more than 20 claims in the last 3 months
3. Identifying customers who made multiple transactions in the last 6 months
4. Extracting dates from timestamp values

### Import datetime module

You can import or load datetime module by using the command below -

```
import datetime
```

You don't need to install this module as it comes bundled with the installation of python software.

## Dates

Here we are using

```
datetime.date
```

class which is used to represent calendar date values.

```
today()
```

method is used to fetch current date.

```
datetime.date.today()

Output
datetime.date(2019, 7, 19)

```

In order to display it like a proper calendar date, we can wrap it within

```
print( )
```

command.

```
print(datetime.date.today())

Output
2019-07-19

```

**Create Date object**

date class follows the syntax as shown below-

> date(year, month, day)
> 

```
dt = datetime.date(2019, 10, 20)

print(dt)

Output
2019-10-20

```

**Extract day, month and year from date values**

```
dt.day
20

dt.month
10

dt.year
2019

```

**Customize Date Formats**

You can customize the format of dates by defining the date formats using

```
strftime
```

method. It converts date objects to strings.

```
dt.strftime("%d-%m-%Y")
Output
20-10-2019

```

```
%d
```

refers to day of the month. In

```
20-10-2019
```

, %d returns 20.

```
%m
```

refers to month of the year. In

```
20-10-2019
```

, %m returns 10.

```
%Y
```

refers to year. The letter 'Y' is in upper case. In

```
20-10-2019
```

, %Y returns 2019.

```
%y
```

refers to year in two-digit format. In

```
20-10-2019
```

, %y returns 19.

**Other popular format codes**

- `%a` returns the first three letter of the weekday `Sun`
- `%A` returns the complete name of the weekday `Sunday`
- `%b` returns the first three letters of the month `Oct`
- `%B` returns the complete name of the month `October`

```
dt.strftime("%d/%m/%Y")
20/10/2019

dt.strftime("%b %d, %Y")
Oct 20, 2019

dt.strftime("%B %d, %Y")
October 20, 2019

dt.strftime("%a %B %d, %Y")
Sun October 20, 2019

dt.strftime("%A %B %d, %Y")
Sunday October 20, 2019

dt.strftime("%A, %B %d, %Y")
Sunday, October 20, 2019

```

## Time

Time values are defined with

```
datetime.time
```

class. It follows the syntax as shown below -

> datetime.time(hour, minute, second, microseconds)
> 

```
t = datetime.time(21, 2, 3)
print(t)
21:02:03

```

**How to get hour, minute and seconds from time values**

```
t.hour
21

t.minute
2

t.second
3

t.microsecond
0

```

**How to convert time to AM PM format**

- `%I` converts 24 hour time format to 12 hour format.
- `%p` returns AM PM based on time values.
- `%H` returns hours of the time value.
- `%M` returns minutes of the time value.
- `%S` returns seconds of the time value.

```
t.strftime("%I:%M %p")
09:02 PM

```

## Handle both dates and time

datetime library has another class named

```
datetime.datetime
```

class which is used to represent date plus time. You can call it timestamp.

```
now()
```

or

```
today()
```

method of datetime class is used to extract current date and time.

```
dt = datetime.datetime.now()
print(dt)

Output
2019-07-20 17:05:05.699416

```

```
%c
```

represents locale date and time.

```
%X
```

represents locale time.

```
dt.strftime("%c")
Sat Jul 20 17:05:05 2019

dt.strftime("%A %B %d %X")
Saturday July 20 17:05:05

dt.strftime("%A %B %d %H:%M")
Saturday July 20 17:05

```

**Create datetime object**

The syntax of datetime class is as follows-datetime(year, month, day, hour, minute, second, microsecond)

```
dt = datetime.datetime(2019, 7, 20, 10, 51, 0)
print(dt)
2019-07-20 10:51:00

dt.strftime('%d-%m-%Y %H-%M')
20-07-2019 10-51

```

**How to convert a string to datetime in python?**

```
from dateutil.parser import parse
print(parse('March 01, 2019'))

2019-03-01 00:00:00

```

## How to get current time?

We can use the same function we used in the previous section and extract time from the returned value using

```
time()
```

method.

```
print(dt.time())

```

## How to get current day of the week?

Suppose you want to extract the day number. 1 for Monday and 7 for Sunday. In the example below it returns 6 as it's Saturday on 20th July, 2019.

```
dt.isoweekday()

```

## Calculate future or past dates

With the use of

```
timedelta
```

, you can add or subtract days, weeks, hours, minutes, seconds, microseconds and milliseconds. It is 
very useful when you want to calculate future or past dates. Suppose you are asked to identify all the customers who enrolled to product in the last 30 days. To solve this, you need to compute the date which is 30 days before the today's date.

```
#30 days ahead
delta = datetime.timedelta(days=30)
print(dt + delta)
2019-08-19 10:51:00

#30 days back
print(dt - delta)
2019-06-20 10:51:00

delta = datetime.timedelta(days= 10, hours=3, minutes=30, seconds=30)
print(dt + delta)
2019-07-30 14:21:30

delta = datetime.timedelta(weeks= 4, hours=3, minutes=30, seconds=30)
print(dt + delta)
2019-08-17 14:21:30

```

In

```
timedelta
```

, months and years options are missing which means you cannot calculate future dates increment by month(s) or year(s). To accomplish this task, we can use

```
dateutil
```

package. Let's import this package by submitting the code below -

```
from dateutil.relativedelta import *
```

If it's not installed on your system, install it by running this command

```
pip install python-dateutil
```

```
#1 Month ahead
print(dt + relativedelta(months=+1))
2019-08-20 10:51:00

#1 Month Back
print(dt + relativedelta(months=-1))

```

If you are wondering how this

```
relativedelta(months=+1)
```

is different from

```
datetime.timedelta(days=30)
```

, observe the returned values (result) of both the commands. Since July has 31 days, 30 days ahead using this

```
datetime.timedelta(days=30)
```

returns

**2019-08-19 10:51:00**

.

```
relativedelta(months=+1)
```

returns

**2019-08-20 10:51:00**

which is a complete 1 month.

```
#Next month, plus one week
print(dt + relativedelta(months=+1, weeks=+1))

#Next Year
print(dt + relativedelta(years=+1))

```

### Consider Leap Years

relativedelta method from dateutil package takes care of leap year while calculating future or past dates. Year 2000 was a leap year so there were 29 days in the February month. But next year has only 28 days in February.

```
print(datetime.date(2000, 2, 29)+ relativedelta(years=+1))

Output
2001-02-28

```

## Difference between Two Dates

Suppose you need to calculate the number of days between two dates. It is a very common data problem statement when you need to calculate the tenure of customers given the information - when they opened their account(start date) and when the accounts got closed (end date).

```
date1 = datetime.date(2020, 10, 25)
date2 = datetime.date(2019, 12, 25)
diff = date1- date2
diff.days

Output
305

```

How would you calculate the number of months between two dates?

One way is to calculate number of days and then divide it by 30 to get number of months. But it is not always correct as some months have 31 days.

**`Not full-proof Solution**
int(diff.days/30)`

**`Correct Solution**
date1.month - date2.month + 12*(date1.year - date2.year)`

**How it works?**

- date1.month - date2.month returns -2
- 12*(date1.year - date2.year) returns 12
- 2 + 12 = 10

> Important Point
> 

## How to work with dates on pandas dataframe?

In real-world, we generally import data from external files and store it in [pandas](https://www.listendata.com/2017/12/python-pandas-tutorial.html) DataFrame. Hence it is important to understand how we perform date and time operations on DataFrame. Let's create a sample dataframe for illustration purpose.

```
df=pd.DataFrame({"A":["2019-01-01", "2019-05-03", "2019-07-03"],
                 "B":["2019-03-02", "2019-08-01", "2019-10-01"] })

```

Let's check the column types.

```
df.dtypes
```

Here both columns A and B are strings (character values).

```
A    object
B    object
dtype: object

```

It is required to convert the columns to

```
datetime
```

object since these variables are stored in string.

```
df['A'] = pd.to_datetime(df['A'])
df['B'] = pd.to_datetime(df['B'])
df.dtypes

A    datetime64[ns]
B    datetime64[ns]
dtype: object

```

In order to calculate the number of days using columns A and B on pandas dataframe, you just need to take a difference of these two columns.

```
df['C'] = df['B'] - df['A']

          A          B       C
0 2019-01-01 2019-03-02 60 days
1 2019-05-03 2019-08-01 90 days
2 2019-07-03 2019-10-01 90 days

```

The column C we have computed is in datetime format. In order to get the difference value in integer format, you can submit the command below.

```
dt
```

enables pandas to use datetime methods.

```
df['C'] = (df['B'] - df['A']).dt.days
df

          A          B   C
0 2019-01-01 2019-03-02  60
1 2019-05-03 2019-08-01  90
2 2019-07-03 2019-10-01  90

```

### Get 3 months past date

The pure pythonic way is to define function in lambda and it runs on all the rows.

```
from dateutil.relativedelta import *
df['D'] = df["B"].apply(lambda x: x - relativedelta(months=3))

           A          B   C          D
0 2019-01-01 2019-03-02  60 2018-12-02
1 2019-05-03 2019-08-01  90 2019-05-01
2 2019-07-03 2019-10-01  90 2019-07-01

```

Another way is to use built-in function

```
DateOffset
```

of pandas package which adds or subtracts days, months, years, weeks, hours, minutes, seconds, microseconds and nanoseconds.

```
df['D1'] = df['B'] - pd.DateOffset(months=3)
```

Filtering dataframe by date Suppose you want to select only those rows where column B has values greater than 1st May, 2019.

```
df[df['B']>datetime.datetime(2019,5,1)]

```

**Select Data between two dates**

Suppose you want to select rows from pandas dataframe between two dates (let's say between 1st May and 30th September).

> df[df.B.between(datetime.datetime(2019,5,1), datetime.datetime(2019,9,30))]
> 
> 
> **OR**
> 

## How to work with different timezones

Manytimes we have date values in different time zones and we need to convert it to our local timezone. It is not easy to solve this manually. In python, there is a library called

```
pytz
```

for setting and conversion of timezone. You can find all the timezones by submitting this command.

```
import pytz
pytz.all_timezones

```

To set datetime object in a particular timezone (let's say Asia/Kolkata), you can use the parameter called tzinfo for this.

```
dt = datetime.datetime(2019, 7, 20, 10, 10, 0, tzinfo=pytz.timezone('Asia/Kolkata'))

```

To convert it to US/Arizona timezone, we can use the method called astimezone for conversion. If you would observe the date has been changed after conversion as difference between these two timezones is more than 12 hours.

```
print(dt.astimezone(pytz.timezone('US/Arizona')))

Output
2019-07-19 21:17:00-07:00

```
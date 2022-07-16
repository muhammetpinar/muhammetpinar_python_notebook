# Read Data With Python

This tutorial explains how to read a CSV file in python using read_csv function of pandas package. Without use of read_csv function, it is not straightforward to import CSV file with python object-oriented programming. Pandas is an awesome powerful python package for data manipulation and supports various functions to load and import data from various formats. Here we are covering how to deal with common issues in importing CSV file.

---

Install and Load Pandas Package

Make sure you have

[pandas package](https://www.listendata.com/2017/12/python-pandas-tutorial.html)

already installed on your system. If you set up python using Anaconda, it comes with pandas package so you don't need to install it again. Otherwise you can install it by using command

```
pip install pandas
```

. Next step is to load the package by running the following command.

```
pd
```

is an alias of pandas package. We will use it instead of full name "pandas".

```
import pandas as pd
```

### Create Sample Data for Import

The program below creates a sample pandas dataframe which can be used further for demonstration.

```
dt = {'ID': [11, 12, 13, 14, 15],
            'first_name': ['David', 'Jamie', 'Steve', 'Stevart', 'John'],
            'company': ['Aon', 'TCS', 'Google', 'RBS', '.'],
            'salary': [74, 76, 96, 71, 78]}
mydt = pd.DataFrame(dt, columns = ['ID', 'first_name', 'company', 'salary'])

```

**The sample data looks like below -**

```
  ID first_name company  salary
0  11      David     Aon      74
1  12      Jamie     TCS      76
2  13      Steve  Google      96
3  14    Stevart     RBS      71
4  15       John       .      78

```

### Save data as CSV in the working directory

Check working directory before you save your datafile.

```
import os
os.getcwd()

```

Incase you want to change the working directory, you can specify it in under

```
os.chdir( )
```

function. Single backslash does not work in Python so use 2 backslashes while specifying file location.

```
os.chdir("C:\\Users\\DELL\\Documents\\")

```

The following command tells python to write data in CSV format in your working directory.

```
mydt.to_csv('workingfile.csv', index=False)
```

## Example 1 : Read CSV file with header row

It's the basic syntax of read_csv() function. You just need to mention 
the filename. It assumes you have column names in first row of your CSV 
file.

```
mydata = pd.read_csv("workingfile.csv")
```

It stores the data the way It should be as we have headers in the first row of our datafile.
It is important to highlight that

```
header=0
```

is the default value. Hence we don't need to mention the

**header=**

parameter. It means header starts from first row as indexing in python starts from

**0**

. The above code is equivalent to this line of code.

```
pd.read_csv("workingfile.csv", header=0)
```

Inspect data after importing

```
mydata.shape
mydata.columns
mydata.dtypes

```

It returns 5 number of rows and 4 number of columns. Column Names are

```
['ID', 'first_name', 'company', 'salary']
```

See the column types of data we imported. **first_name** and **company** are character variables. Remaining variables are numeric ones.

```
ID             int64
first_name    object
company       object
salary         int64

```

## Example 2 : Read CSV file with header in second row

Suppose you have column or variable names in second row. To read this kind of CSV file, you can submit the following command.

```
mydata = pd.read_csv("workingfile.csv", header = 1)
```

```
header=1
```

tells python to pick header from second row. It's setting second row as header. It's not a realistic example. I just used it for illustration so that you get an idea how to solve it. To make it practical, you can add random values in first row in CSV file and then import it again.

```
11    David     Aon  74
0  12    Jamie     TCS  76
1  13    Steve  Google  96
2  14  Stevart     RBS  71
3  15     John       .  78

```

Define your own column names instead of header row from CSV file

```
mydata0 = pd.read_csv("workingfile.csv", skiprows=1, names=['CustID', 'Name', 'Companies', 'Income'])

```

**skiprows = 1**

means we are ignoring first row and

**names=**

option is used to assign variable names manually.

```
   CustID     Name Companies  Income
0      11    David       Aon      74
1      12    Jamie       TCS      76
2      13    Steve    Google      96
3      14  Stevart       RBS      71
4      15     John         .      78

```

## Example 3 : Skip rows but keep header

```
mydata = pd.read_csv("workingfile.csv", skiprows=[1,2])

```

In this case, we are skipping **second** and **third** rows while importing. Don't forget index starts from 0 in python so 0 refers to first row and 1 refers to second row and 2 implies third row.

```
   ID first_name company  salary
0  13      Steve  Google      96
1  14    Stevart     RBS      71
2  15       John       .      78

```

Instead of **[1,2]** you can also write `range(1,3)`. Both means the same thing but range( ) function is very useful when you want to skip many rows so it saves time of manually defining row position.

**Hidden secret of skiprows option**

When **skiprows = 4**, it means skipping four rows from top. **skiprows=[1,2,3,4]** means skipping rows from second through fifth. It is because when list is specified in skiprows= option, it skips rows at index positions. When a single integer value is specified in the option, it considers skip those rows from top

## Example 4 : Read CSV file without header row

If you specify **"header = None",** python would assign a series of numbers starting from 0 to (number of columns - 1) as column names. In this datafile, we have column names in first row.

```
mydata0 = pd.read_csv("workingfile.csv", header = None)
```

See the output shown below-

![https://2.bp.blogspot.com/-o4DimIV1Cr8/V0xX6O7KPnI/AAAAAAAAEb8/VTpuq2PVLhIyPtvGg32T_tRpdCsT9bFdwCLcB/s1600/sample%2Bdata_python.png](https://2.bp.blogspot.com/-o4DimIV1Cr8/V0xX6O7KPnI/AAAAAAAAEb8/VTpuq2PVLhIyPtvGg32T_tRpdCsT9bFdwCLcB/s1600/sample%2Bdata_python.png)

---

Output

---

Add prefix to column names

```
mydata0 = pd.read_csv("workingfile.csv", header = None,prefix="var")
```

In this case, we are setting

```
var
```

as prefix which tells python to include this keyword before each column name.

```
 var0        var1     var2    var3
0   ID  first_name  company  salary
1   11       David      Aon      74
2   12       Jamie      TCS      76
3   13       Steve   Google      96
4   14     Stevart      RBS      71
5   15        John        .      78

```

## Example 5 : Specify missing values

The

```
na_values=
```

options is used to set some values as blank / missing values while importing CSV file.

```
mydata00 = pd.read_csv("workingfile.csv",na_values=['.'])
```

```
   ID first_name company  salary
0  11      David     Aon      74
1  12      Jamie     TCS      76
2  13      Steve  Google      96
3  14    Stevart     RBS      71
4  15       JohnNaN      78

```

## Example 6 : Set Index Column

```
mydata01 = pd.read_csv("workingfile.csv",index_col ='ID')
```

```
   first_name company  salary
ID
11      David     Aon      74
12      Jamie     TCS      76
13      Steve  Google      96
14    Stevart     RBS      71
15       John       .      78

```

As you can see in the above output, the column ID has been set as index column.

## Example 7 : Read CSV File from External URL

You can directly read data from the CSV file that is stored on a web link. It is very handy when you need to load publicly available datasets from github, kaggle and other websites.

```
mydata02 = pd.read_csv("http://winterolympicsmedals.com/medals.csv")
```

This DataFrame contains 2311 rows and 8 columns. Using

```
mydata02.shape
```

, you can generate this summary.

## Example 8 : Skip Last 5 Rows While Importing CSV

```
mydata04 = pd.read_csv("http://winterolympicsmedals.com/medals.csv", skip_footer=5)
```

*In the above code, we are excluding bottom 5 rows using **skip_footer=** parameter.*

## Example 9 : Read only first 5 rows

```
mydata05 = pd.read_csv("http://winterolympicsmedals.com/medals.csv", nrows=5)
```

Using **nrows=** option, you can load top K number of rows.

## Example 10 : Interpreting "," as thousands separator

```
mydata06  = pd.read_csv("http://winterolympicsmedals.com/medals.csv", thousands=",")
```

## Example 11 : Read only specific columns

```
mydata07 = pd.read_csv("http://winterolympicsmedals.com/medals.csv", usecols=[1,5,7])
```

The above code reads only columns based on index positions which are second, sixth and eighth position.

## Example 12 : Read some rows and columns

```
mydata08 = pd.read_csv("http://winterolympicsmedals.com/medals.csv", usecols=[1,5,7], nrows=5)
```

In the above command, we have combined usecols= and nrows= options. It will select only first 5 rows and selected columns.

## Example 13 : Read file with semi colon delimiter

```
mydata09 = pd.read_csv("file_path", sep =';')
```

Using

**sep=**

parameter in read_csv( ) function, you can import file  with any delimiter other than default comma. In this case, we are using  semi-colon as a separator.

## Example 14 : Change column type while importing CSV

Suppose you want to change column format from int64 to float64 while loading CSV file into Python. We can use **dtype =** option for the same.

```
mydf = pd.read_csv("workingfile.csv", dtype = {"salary" : "float64"})

```

## Example 15 : Measure time taken to import big CSV file

With the use of

```
verbose=True
```

, you can capture time taken for Tokenization, conversion and Parser memory cleanup.

```
mydf = pd.read_csv("workingfile.csv", verbose=True)
```

## Example 16 : How to read CSV file without using Pandas package

To import CSV file with pure python way, you can submit the following command :

```
import csv
with open("C:/Users/DELL/Downloads/nycflights.csv") as f:
  d = DictReader(f)
  l=list(d)

```

You can also download and load CSV file from URL or external webpage.

```
import csv
import requests

response = requests.get('https://dyurovsky.github.io/psyc201/data/lab2/nycflights.csv').text
lines = response.splitlines()
d = csv.DictReader(lines)
l = list(d)

```

EndNote After completion of this tutorial, I hope you gained confidence in importing CSV file into Python with ways to clean and manage file. You can also check out this [tutorial](https://www.listendata.com/2017/02/import-data-in-python.html) which  explains how to import files of different format to Python. Once done, you should learn how to perform common data manipulation or wrangling tasks like filtering, selecting and renaming columns, identify and remove duplicates etc on pandas dataframe.

This tutorial explains various methods to read data in Python. Data can be in any of the popular formats - CSV, TXT, XLS/XLSX (Excel), sas7bdat (SAS), Stata, Rdata (R), etc. Loading data in a python environment is the initial step of analyzing data.

---

Import Data into Python

---

***While importing external files, we need to check the following points -***

1. Check whether header row exists or not
2. Treatment of special values as missing values
3. Consistent data type in a variable (column)
4. Date Type variable in consistent date format.
5. No truncation of rows while reading external data

---

Install and Load pandas Package

**pandas**

is a powerful data analysis package. It makes data exploration and manipulation easy. It has several functions to read data from various sources.

If you are using **Anaconda**, pandas must be already installed. You need to load the package by using the following command -import pandas as pd If pandas package is not installed, you can install it by running the following code in **Ipython Console.** If you are using **Spyder,**you can submit the following code in Ipython console within Spyder.

> !pip install pandas
> 

If you are using

**Anaconda**

, you can try the following line of code to install pandas -

> !conda install pandas
> 

## 1. Import CSV files

It is important to note that **a single backslash does not work** when specifying the file path**.**

You need to either **change it to forward slash or add one more backslash** like below

> import pandas as pd
> 

### If no header (title) in raw data file

> mydata1 = pd.read_csv("C:\\Users\\Deepanshu\\Documents\\file1.csv",**header = None)**
> 

You need to include

**header = None**

option to tell Python there is no column name (header) in data.

### Add Column Names

We can include column names by using names= option.

> mydata2 = pd.read_csv("C:\\Users\\Deepanshu\\Documents\\file1.csv", header = None,
> 
> 
> **names = ['ID', 'first_name', 'salary']**
> 

### The variable names can also be added separately by using the following command.

> mydata1.columns = ['ID', 'first_name', 'salary']
> 

[Detailed Explanation : Import CSV File in Python](https://www.listendata.com/2019/06/pandas-read-csv.html)

## 2. Import File from URL

You don't need to perform additional steps to fetch data from URL. Simply put

**URL**

in read_csv() function (applicable only for CSV files stored in URL).

> mydata = pd.read_csv("http://winterolympicsmedals.com/medals.csv")
> 

## 3. Read Text File

We can use read_table() function to pull data from text file. We can also use read_csv() with sep= "\t" to read data from tab-separated file.

> mydata  = pd.read_table("C:\\Users\\Deepanshu\\Desktop\\example2.txt")
> 

## 4. Read Excel File

The read_excel() function can be used to import excel data into Python.

> mydata = pd.read_excel("https://www.eia.gov/dnav/pet/hist_xls/RBRTEd.xls",sheetname="Data 1", skiprows=2)
> 

*If you do not specify name of sheet in **sheetname= option**, it would take by default first sheet.*

## 5. Read delimited file

Suppose you need to import a file that is separated with white spaces.

> mydata2 = pd.read_table("http://www.ssc.wisc.edu/~bhansen/econometrics/invest.dat",
> 
> 
> **sep="\s+"**
> 

To include variable names, use the names= option like below -

> mydata3 = pd.read_table("http://www.ssc.wisc.edu/~bhansen/econometrics/invest.dat", sep="\s+", names=['a', 'b', 'c', 'd'])
> 

## 6. Read SAS File

We can import SAS data file by using read_sas() function.

> mydata4 = pd.read_sas('cars.sas7bdat')
> 

If you have a large SAS File, you can try package named

```
pyreadstat
```

which is faster than pandas. It is equivalent to

```
haven
```

package in R which provides easy and fast way to read data from SAS, SPSS and Stata. To install this package, you can use the command

```
pip install pyreadstat
```

```
import pyreadstat
df, meta = pyreadstat.read_sas7bdat('cars.sas7bdat')

# done! let's see what we got
print(df.head())
print(meta.column_names)
print(meta.column_labels)
print(meta.number_rows)
print(meta.number_columns)

```

## 7. Read Stata File

We can load Stata data file via read_stata() function.

> mydata41 = pd.read_stata('cars.dta')
> 

```
pyreadstat
```

package lets you to pull value labels from stata files.

```
import pyreadstat
df, meta = pyreadstat.read_dta("cars.dta")

```

To get labels, set

```
apply_value_formats
```

as

**TRUE**

```
df, meta = pyreadstat.read_dta("cars.dta", apply_value_formats=True)

```

## 8. Import R Data File

Using **pyreadr** package, you can load**. RData** and**.Rds** format files which in general contains R data frame. You can i**nstall this package** using the command below -

pip install pyreadr

With the use of

**read_r( )**

function, we can import R data format files.

> import pyreadr
> 

*Similarly, you can read **.Rds** formatted file.*

## 9. Read SQL Table

We can extract table from SQL database (SQL Server / Teradata). See the program below -SQL Server You can read data from tables stored in SQL Server by building a connection. You need to have server, User ID (UID), database details to establish connection.

```
import pandas as pd
import pyodbc
conn = pyodbc.connect("Driver={SQL Server};Server=serverName;UID=UserName;PWD=Password;Database=RCO_DW;")
df = pd.read_sql_query('select * from dbo.Table WHERE ID > 10', conn)
df.head()

```

Teradata You need to import **Teradata module** which makes python easily integrated with Teradata Database.

```
import pandas as pd
import teradata
udaExec = teradata.UdaExec(appName="HelloWorld", version="1.0",
                           logConsole=False)
session = udaExec.connect(method="odbc",
                          USEREGIONALSETTINGS="N",
                          system="tdprod",
                          username="xxx",
                          password="xxx");

query = "SELECT * FROM flight"
df = pd.read_sql(query , session)

```

Explanation

- `UdaExec` provides DevOps support features such as configuration and logging.
- You can assign any name and version in `appName` and `version`
- `logConsole=False` tells Python not to log to the console.
- `system="tdprod"` refers to name of the system we are connecting using ODBC as the connection method
- `USEREGIONALSETTINGS="N"` is used to ensure that float values can be loaded and make decimal separator be ‘.’

Suppose you have

```
.db
```

extension file which is a database file and you want to extract data from it.

> import sqlite3
> 

## 10. Import Data from SPSS File

```
import pyreadstat
df, meta = pyreadstat.read_sav("file.sav", apply_value_formats=True)

```

If you don't want value labels, make **apply_value_formats** as False.

## 11. Read sample of rows and columns

By specifying nrows= and usecols=, you can fetch the specified number of rows and columns.

> mydata7 = pd.read_csv("http://winterolympicsmedals.com/medals.csv",
> 
> 
> **nrows**
> 
> **usecols**
> 

nrows = 5 implies you want to import only first 5 rows and usecols= refers to specified columns you want to import.

## 12. Skip rows while importing

Suppose you want to skip first 5 rows and wants to read data from 6th row (6th row would be a header row)

> mydata8 = pd.read_csv("http://winterolympicsmedals.com/medals.csv",
> 
> 
> **skiprows**
> 

## 13. Specify values as missing values

By including na_values= option, you can specify values as missing values. In this case, we are telling python to consider dot (.) as missing cases.

> mydata9 = pd.read_csv("workingfile.csv", na_values=['.'])
>
# OOP-Classes in Python: Fundamentals for Data Science

# **Defining the Classes**

In our example, I will be using [Pandas](https://pandas.pydata.org/), which is a popular data manipulation library for Python, together with several [CSV files](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks) containing tabular data.

In Python, the basic class definition has the following format;

```python
classClassName():
 # Comments / Notes
 ...
 # Initializer / Instance Attributes
 ...
 # Methods
 ...
```

To start, let’s create a simple class that helps us to display summary information of the tabular data contained in a CSV file.

```python
class CSVGetInfo:
""" This class displays the summary of the tabular data contained in a CSV file """
def__init__(self,path,file_name):
 self.path = path
 self.file_name = file_name
def display_summary(self):
 data = pd.read_csv(self.path + self.file_name)
 print(self.file_name)
 print(data.info())
```

In Python, a simple class definition starts with the following notation:

```
class ClassName:
```

In our example, our class name is **“CSVGetInfo”**. Please note that class names in Python follow **UpperCaseCamelCase** naming convention. Although it is not mandatory, it is common to store the classes in a separate file and import them later when needed.

It is a good practice to add a comment section to let others know what our class does. We can do this by providing our notes inside the triple double-quotes.

```python
class CSVGetInfo:
""" This class displays the summary of the tabular data contained in a CSV file """
```

# **Initialising the Instance Variables (Attributes)**

After these first steps, it is now time to define the data involved with our class. In our example, we need to know the path and file name information of the CSV file we want to read.

So, our class has **‘path’** and **‘file_name’** variables. They will be initialised for every instance of our **CSVGetInfo** class and they are called as instance variables or attributes of our class.

```python
# Initializer / Instance Attributes
def __init__(self,path,file_name):
  self.path = path
  self.file_name = file_name
```

**__init__** method indicates what data must be supplied when we create a new instance of our class.

The data supplied with the local variables to be stored in ***self.path*** and ***self.file_name.*** Here, *self* represents the instance itself.

Variable initialisation is a mandatory process while creating the instances, and this special **__init__** method guarantees that it happens all the time.

# **Adding Instance Functions (Methods)**

Now, we can define functions that use this data to handle specific tasks. Functions in a class structure called as methods or instance functions, as they are tied up every instance of the class. We will define **“display_summary”** method in our **CSVGetInfo** class structure, which displays the summary information of tabular data contained in a CSV file.

```python
# Methodsdefdisplay_summary(self):
 data = pd.read_csv(self.path + self.file_name)
 print(self.file_name)
 print(data.info())
```

Note that we have again used *self* in our method as a parameter. This is needed to access the data contained in the instance we are working on.

To access the instance variables inside the **“display_summary”** method, we use self.path and self.file_name notation.

# **Creating Instances of Classes (Objects)**

As the class itself is the blueprint of the objects, we need to create instances of the class (objects) to handle the tasks using the methods available in the class definition.

In our class, we have the **“display_summary”** method.

So let’s create two instances of **CSVGetInfo** and use **“display_summary”** method to see what is inside the CSV files.

To create instances/objects of a class, we use the class name and we pass the values to parameters required for the class.

```python
data_by_artists = CSVGetInfo("/Users/erdemisbilen/Lessons/", "data_by_artists.csv")
data_by_genres = CSVGetInfo("/Users/erdemisbilen/Lessons/", "data_by_genres.csv")
```

Now the variable **data_by_artist** holds the reference to the first instance of our **CSVGetInfo** class. It is an object/instance of **CSVGetInfo** class which stores the value of **“data_by_artists.csv”** in the **file_name** (instance variable). Other ****variable **data_by_genres** holds the reference to the second instance of our class which has **“data_by_genres.csv”** value stored in the **file_name**. Although they are created with the same class definition, they have different values stored in the instance variables(attributes).

```python
print(data_by_artists)
print(data_by_genres)#Output
<__main__.CSVGetInfo instance at 0x10b84f248>
<__main__.CSVGetInfo instance at 0x114eb58c0>
```

When we print the instances, we can see that they are stored at different locations in the memory.

**Let’s use “display_summary” method.**

```python
**data_by_artists.display_summary()
data_by_genres.display_summary()#Output
data_by_artists.csv
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 27606 entries, 0 to 27605
Data columns (total 15 columns):
artists             27606 non-null object
acousticness        27606 non-null float64
danceability        27606 non-null float64
duration_ms         27606 non-null float64
energy              27606 non-null float64
instrumentalness    27606 non-null float64
liveness            27606 non-null float64
loudness            27606 non-null float64
speechiness         27606 non-null float64
tempo               27606 non-null float64
valence             27606 non-null float64
popularity          27606 non-null float64
key                 27606 non-null int64
mode                27606 non-null int64
count               27606 non-null int64
dtypes: float64(11), int64(3), object(1)
memory usage: 3.2+ MB
Nonedata_by_genres.csv
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2617 entries, 0 to 2616
Data columns (total 14 columns):
genres              2617 non-null object
acousticness        2617 non-null float64
danceability        2617 non-null float64
duration_ms         2617 non-null float64
energy              2617 non-null float64
instrumentalness    2617 non-null float64
liveness            2617 non-null float64
loudness            2617 non-null float64
speechiness         2617 non-null float64
tempo               2617 non-null float64
valence             2617 non-null float64
popularity          2617 non-null float64
key                 2617 non-null int64
mode                2617 non-null int64
dtypes: float64(11), int64(2), object(1)
memory usage: 286.3+ KB
None**
```

[Automated Data Cleansing](OOP-Classes%20in%20Python%20Fundamentals%20for%20Data%20Scienc%20a2cd50b349f14cf8879a3a08cb789c1e/Automated%20Data%20Cleansing%20626535fb2507496cadf1a5a0e18a2336.md)

[**prepare data for modeling**](OOP-Classes%20in%20Python%20Fundamentals%20for%20Data%20Scienc%20a2cd50b349f14cf8879a3a08cb789c1e/prepare%20data%20for%20modeling%204c27db91ab274ac49a339bb04612730b.md)
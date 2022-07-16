# Basics of EDA

genel bilgi almak için

`# get initial information from data
from utils.utils import initial_information
initial_information(df)`

## **1. Check data shape (num of Rows & Columns)**

This can be done by just simply use, the code down below

```
df.shape
Output sample:
(821534,14)
```

The  output will give you the information on the number of rows and columns in your dataset. In the example above, there are 821,534 rows and 14 columns in the data. One of these 14 columns is a dependent variable which usually will be used as a target column for analysis with machine learning later. The rest of them are mostly independent variables.

## **2. Check each data type of columns and missing values**

```
df.info()
```

The output will usually be like this:

![https://miro.medium.com/max/826/0*LQnmRWK47rlDP8bL.PNG](https://miro.medium.com/max/826/0*LQnmRWK47rlDP8bL.PNG)

Source: Google Images

Here as we can see, there are 7,787 rows with 12 columns. From these 12 columns, **several columns have missing values** which are **director**, **cast**, **country**, **date_added**, and **rating.**

For the data type, we only have object and integer here. However, if we see in **column date_added**, it **should have a data type of datetime, right? not an object data type.** We will correct this data type into datetime later in the next steps.

## 3. Splitting values

On  some occasions, we might want to split the value of a column. For example, there is an address column that includes city and country. We want to split it into two columns which column of city and country.

```
   name      age    address
0  anton    24    London,UK
1  sarah    30    New York,US
2  tom      23    Darwin,Australia
3  katie    24    Paris,France
4  john     27    Hamburg,Germany
```

This can be achieved by using the following code:

```
df[['city', 'country']] = df['address'].str.split(',', expand=True)Out[10]:
  name      age    address           city      country
0  anton    24    London,UK         London      UK
1  sarah    30    New York,US       New York    US
2  tom      23    Darwin,Australia  Darwin      Australia
3  katie    24    Paris,France      Paris       France
4  john     27    Hamburg,Germany   Hamburg     Germany
```

## 4. Change the data type

We  can use astype() function from pandas. For example, I want to replace the data type of Customer Number, IsPurchased, Total Spend, and Dates

```
#Replace Data Types to Integer
df["Customer Number"] = df['Customer Number'].astype('int')#Replace Data Types to String
df["Customer Number"] = df['Customer Number'].astype('str')#Replace Data Types to Boolean
df["IsPurchased"] = df['IsPurchased'].astype('bool')#Replace Data Types to Float
df["Total Spend"] = df['Total Spend'].astype('float')#Replace Data Types to Datetime with format= '%Y%m%d'
df['Dates'] = pd.to_datetime(df['Dates'], format='%Y%m%d')
```

## **5. Check the percentages of missing value**

I
 am personally often doing this so I can have a clear reason to drop or  dealing with the missing values. If the percentage of missing values is high and it is not an important column, I sometimes just dropped the corresponding column😬.

```
df.isnull().sum() / df.shape[0] * 100
```

![https://miro.medium.com/max/938/1*5qSFG3cQ_lJ7xFFp-Wzstw.png](https://miro.medium.com/max/938/1*5qSFG3cQ_lJ7xFFp-Wzstw.png)

We can see that **SHOOTING and UCR_PART variables have the highest percentages of missing values** more than and nearly 50% of the total values. Thus, for this case, **I just droped these two columns**
 as they are also not important columns that need to be used for the analytical process. For the rest of the columns like OFFENSE_CODE_GROUP.
 I just replaced the missing values with the value from OFFENSE_CODE as it has similar values.

## 6. Summary Statistics

```
df.describe()
```

Output:

![https://miro.medium.com/max/1400/0*3PsvCYRCWvhDitVt.png](https://miro.medium.com/max/1400/0*3PsvCYRCWvhDitVt.png)

This  function from pandas is used to return the count, mean std, min, quartiles, and max. From this, you could already see the data distribution that you have for each and determine whether there are 
outliers or not.

## 7. Check value counts for a specific column

Here I want to see counts of each value in Player column in the dataset.

```
#check Player data
df.Player.value_counts()
```

Output:

![https://miro.medium.com/max/1026/1*H4liv5-793HIfwx3AVBS4g.png](https://miro.medium.com/max/1026/1*H4liv5-793HIfwx3AVBS4g.png)

I  sometimes use this function to see if there are duplicate values in the  column. We can see here that there is more than 1 value in several players.

## **8. Check duplicate values and deal with it**

Once we know that there are several player that occurred more than 1 in the dataset. We need to do further investigation using the following code; 
Take consideration to Player named “Ersan Ilyasova”.

```
#example of the data that have multiple values
df[df.Player == "Ersan Ilyasova"]
```

Output:

![https://miro.medium.com/max/1400/1*oniFkIlx2KcKn-cSQ9jFPg.png](https://miro.medium.com/max/1400/1*oniFkIlx2KcKn-cSQ9jFPg.png)

This code will give all information from every column for each value. **Next, we need to determine which one do we want to keep.**
 It could be based on the latest, older value, or any. It can be done by  using this code; for example; I want to keep the value in the first row.

```
#drop duplicates values and keep the first records from duplicates
#with an assumption that the first row contains the latest data

df = df.drop_duplicates("Player", keep='first')
df= df.reset_index(drop=True)
```

## 9. See the data distribution and data anomaly

From the summary statistics before, we might already know which columns that  potentially having data anomalies. Here, we want to see visually how the data distribution is using the Seaborn library.

```
#plot the histogram to see the distribution of the point data.
sns.displot(data, x="age")
```

![https://miro.medium.com/max/1090/1*cjiqxe9HTiMvfsN8APtTEQ.png](https://miro.medium.com/max/1090/1*cjiqxe9HTiMvfsN8APtTEQ.png)

If you want to measure the skewness and kurtosis of the distribution, you can use the code down below;

```
#measure its skewness and kurtosis
data['age'].agg(['skew', 'kurtosis']).transpose()output(example):
skew        0.609893
kurtosis    0.432258
Name: general_points, dtype: float64
```

We  see here that the age distribution was skewed to the right. Now, Let’s check the outlier for the total_bill column with Boxplot.

```
ax = sns.boxplot(x=data["total_bill"])
```

![https://miro.medium.com/max/928/0*W2xLCWtowtd68FO2.png](https://miro.medium.com/max/928/0*W2xLCWtowtd68FO2.png)

It  can be seen clearly that outliers were starting after 40. It is up to you to deal with outliers. You can drop the outliers or do data transformation. Here, I put the options that you can do to transform 
non-normal distributions.

![https://miro.medium.com/max/1400/1*_aN1iaiVUTdoyPbyj-kVjA.jpeg](https://miro.medium.com/max/1400/1*_aN1iaiVUTdoyPbyj-kVjA.jpeg)

## 10. Check the correlation between variables in the data

Checking  the correlation between variables is also necessary to see potential a feature that we can use for further analysis or building a model later. 
We can use a correlation matrix to get this.

First, create a variable that holds or has the dataframe value.

```
corrMatrix = df.corr()
```

Next, we visualise the matrix with Seaborn library

```
sns.heatmap(corrMatrix, annot = True, cmap= 'coolwarm')
```

Output:

![https://miro.medium.com/max/1072/1*Be2rDBr3x7OpNnMS7cKITA.png](https://miro.medium.com/max/1072/1*Be2rDBr3x7OpNnMS7cKITA.png)
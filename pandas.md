# Pandas Learning

# Data Frame

## Inspecting a data frame

.head()n d
returns the first five rows

.info() 
shows information on each of the columns, such as the data type and number of missing values

.shape 
returns the number of rows and columns. Remember its an attribute not a function and hence needs no brackets

.describe() 
calculates a summary of the statistics for each column

## Parts of a dataframe

.values: 
A two-dimensional NumPy array of values

.columns: 
An index of columns: the column names

.index: 
An index for the rows: either row numbers or row names

# Sorting and Subsetting data

## Sorting Rows

one column	
df.sort_values("name of column")
to change in descending order
df.sort_values(["name of column"],ascending=[False])

multiple columns	
df.sort_values(["column 1", "column 2"])
To change orders
df.sort_values(["column 1", "column 2"],ascending=[True, False])

## Subsetting Columns

One Column
df["col_a"]

Two columns
df[["col_a", "col_b"]]   * dont forget two square brackets

## Subsetting rows

df[df["column name"] > 60]
df[df["column name"] == "attribute"]
df[(df["cl1"] > 60) & (df["cl2"] == "attribute")]
df[(df["col"] == "value_1") | (df["col"] == "value_2")]

attributedf = ["a1", "a2", "a3"]
condition = df["column"].isin(attributedf)
df[condition]
df[df["col"].isin(["value_1", "value_2"])]

## Dropping duplicate names
df.drop_duplicates(subset='column_name') 

## Dropping duplicate pairs
df.drop_duplicates(subset=['column_name1','column_name2')

## Getting unique values of a column

df1=df["column"].unique()
print(df1)

## Adding new columns

df['new column'] = df['cl1] + df[cl2]
df['new column'] = df['cl1] /100

# Summary Statistics

Mean
df['column-name'].mean()

Median
df['column-name'].median()

Mode
df['column-name'].mode()

Minimum
df['column-name'].min()

Maximum
df['column-name'].max()

You can use min and max functions to get the oldest and latest dates

Variance
df['column-name'].var()

Standard Deviation
df['column-name'].std()

Sum
df['column-name'].sum()

The .agg() method
def pct30(column):
    return column.quantile(0.3)
- To calculate the 30th percentile   for example 

df['column-name'].agg(pct30)

agg can be used on multiple columns

It can also be used for multiple summaries
df['column-name'].agg([pct30,pct40])

Cumulative Sum
df['column-name'].cumsum()

Cumulative Maximum
df['column-name'].cummax()

Cumulative Minimum
df['column-name'].cummin()

Cumulative Product
df['column-name'].cumprod()

Summary Statistics for groups

df.groupby("column_name")['Column_2'].mean()

For multiple Statistics
df.groupby("column_name")['Column_2'].agg(min,max,sum)

Multiple columns
df.groupby(["column_name","column_name"])['Column_2'].agg(min,max,sum)

## Pivot Table
df.pivot_table(values="column1",index="column2")
default mean
To change - df.pivot_table(values="column1",index="column2", aggfunc=np.median)
multiple functions - df.pivot_table(values="column1",index="column2", aggfunc=[np.mean,np.median])

Two variables
df.pivot_table(values="column1",index="column2", columns = "column3")

nan is due to missing values
to fill in values 
df.pivot_table(values="column1",index="column2", columns = "column3", fill_value=0)
for adding mean
df.pivot_table(values="column1",index="column2", columns = "column3", fill_value=0, margins=True)



## To count number of items in columns
df['column_name'].value_counts()

To sort
df['column_name'].value_counts(sort=True)

To calculate proportions from total
df['column_name'].value_counts(normalize=True)

to calculate proportions and sort
df['column_name'].value_counts(sort=Ture,normalize=True)

# Explcit Indexes

Explicit indexes
DataFrames are composed of three parts: 
a NumPy array for the data, 
and two indexes to store the row and column details

.columns
Index object of column names
.index
Index object of row numbers

how to set a column as the index
df_ind = df.set_index("column1")

df = pd.read_csv("df.csv", index_col=["column"])
df = pd.read_csv("df.csv", index_col=["column","column"])

how to remove an index
df_ind.reset_index()

how to drop an index
df_ind.reset_index(drop=True)

how to set a multilevel index
1. Set hierarchical index
df_ind = df.set_index(["column_h1","column_h2"])
rows_to_keep = [("Ch1_attribute","Ch2_attribute"),("Ch1_attribute","Ch2_attribute")]
print(df_ind.loc[rows_to_keep])

Indexes make subsetting simpler

Sorting by index values

> Sort df by index values
print(df.sort_index())

> Sort df by index values at the column level
print(df.sort_index(level="column"))

> Sort df by column1 then descending column2
print(df.sort_index(level=["column1", "column1"], ascending = [True, False]))

## Subsetting using loc
df.loc["column_name"]
Without an index, subsetting takes the form 
df[df["column"].isin(values)]
With an index, subsetting takes the form 
df_ind.loc[values]

## Slicing and subsetting using loc and iloc

Slicing Lists

df= [a,b,c,d,e]
df[2:4]

Slicing Data Frames
First Sort Index
df = df.set_index(['column1','column2']).sort_index()

Slicing out rows at index level

df.loc['row1':'row3']
final value row 3 will be included
does not work on inner index level

To slice inner index correctly
df.loc[('row1','row1correspondingrowvalue":'row3'),('row1correspondingrowvalue")]

Slicing columns
df.loc[:,'columnname']

Slicing rows and columns
df.loc[('row1','row1correspondingrowvalue":'row3','row1correspondingrowvalue"),"column1":"column3"]

Subsetting by row/column no
df.iloc[2:5 , 1:3]

Compared to slicing lists, there are a few things to remember.

You can only slice an index if the index is sorted (using .sort_index()).
To slice at the outer level, first and last can be strings.
To slice at inner levels, first and last should be tuples.
If you pass a single slice to .loc[], it will slice the rows.

## Pivoting Tables

pv_df = df.pivot_table("column", index='row',columns='columns')
default aggregation in mean

you can use .loc[] function on pv_df

The axis argument
pv_df.mean(axis='index')   across columns
pv_df.mean(axis='columns')   across rows

## Missing Values
Nan - not a number

## Detecting missing values
All missing values
df.isna()

Any missing values in column
df.isna().any()

Counting missing values in column
df.isna().sum()

Counting null value in column
df.isnull().sum()

How to visualize missing data using a bar plot
import matplotlib.pyplot as plt
df.isna().sum().plot(kind="bar")
plt.show()

Removing rows that contain missing values
df.dropna()
Not ideal if there is a lot of data

Replacing missing values with another value
df.fillna(0)

## Creating Data Frames
pd.DataFrame(Name of list/Name of Dictionary)

## Writing and Reading CSV
new_file = pd.read_csv('nameoffile.csv')

adding new column
file['name of column'] = file["onevalue"]/file["another value"], etc

new file 
new_file.to_csv(""new_name.csv")
dt.to_csv('C:/Users/abc/Desktop/file_name.csv')

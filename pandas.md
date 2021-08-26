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

## To count number of items in columns
df['column_name'].value_counts()

To sort
df['column_name'].value_counts(sort=True)

To calculate proportions from total
df['column_name'].value_counts(normalize=True)

to calculate proportions and sort
df['column_name'].value_counts(sort=Ture,normalize=True)


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

## Sorting and Subsetting data

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

attributedf = ["a1", "a2", "a3"]
condition = df["attribute"].isin(attributedf)
df[condition]

# Inner Join

df_merge = df.merge(df2, on="common column")

Use suffix to show what table the column originates from
To control suffix
df_merge = df.merge(df2, on="common column",suffixes=('_df','_df2'))

df_merge = df.merge(df2, on="common column", how="inner")

If columns are named differently
df_merge = df.merge(df2, left_on="column", right_on="column")


## Merging using two columns

df_merge = df.merge(df2, on=["column1",'column2'])


## Merging more than one table

df_merge = df.merge(df2, on="common column") \ .merge(df3, on="comon column")

## Left Joint

A left join returns all rows of data from the left table and only those rows from the right table where key columns match.

df_merge = df.merge(df2, on = 'common column', how="left")

## Other joins

## Right join 
 It will return all of the rows from the right table and includes only those rows from the left table that have matching values. It is the mirror opposite of the left join

 df_merge = df.merge(df2, on = 'common column', how="right")


## Outer join
 An outer join will return all of the rows from both tables regardless if there is a match between the tables
 df_merge = df.merge(df2, on = 'common column', how="outer")


## Self join
df_merge = df.merge(df, left_on="column", right_on="column", suffixes=("_df_merge","_df"))
you can use different types of joins for this
When can a talbe be merged to itself - hierarchical data, sequential data, graphical data

## Merging on indexes

set the column as index
df_merge = df.merge(df2, on="column",how="left")

if index names are different in the tables then you can use left_on and right_on arguments of the merge method
df_merge = df.merge(df2, left_on="column", left_index=True,right_on="column", right_index=True)

## Filtering joins

Mutating Joins - combines data from two tables based on matching observations in both tables
Filtering joins - Filter observations from tables based on whether or not they match an obeservation from another table

## Semi joins

Returns intersection, similar to an inner join
Returns only columns from the left table and not the right table
No duplicate rows from the left table are returned

ex
# Merge columns
df_merge = df.merge(df2, on='column', 
                                 how='left', indicator=True)

# Select the column where _merge is left_only
column_list = df_merge.loc[df_merge['_merge'] == 'left_only', 'column']

# get no coinciding data
print(df[df['column'].isin(column_list)])

## Anti Join
Returns the left table, excluding the intersection
Returns only columns from the left table

## Concatenate two tables vertically

Basic concatenate
pd.concat([column1,column2,column3])

To ignore index
pd.concat([column1,column2,column3],ignore_index=True)

Setting lables to original tables
pd.concat([column1,column2,column3],
           ignore_index=False,
           keys=['c1','c2','c3'])
You cannot add a key and ignore the index at the same time

To concatenate tables with different column names 
If you want all columns
pd.concat([c1,c2],sort=True)
If you want only matching columns
pd.concat([c1,c2],join="inner")

Using .append() method
It supports ignore_index and sort 
but not keys and join(join is "outer" by default)

c1.append([c2,c3],ignore_index=True,sort=True)

## Verifying integrity

.merge(validate=        )

'one_to_one'
'one_to_many'
'many_to_one'
'many_to_many'

Verifying concatenations

.concat(verify_integrity=False)
default is false
if set to true, it will check if there are duplicate values in the index and raise an error

## Using merge_order()
The results are similar to the standard merge method with an outer join, but here that the results are sorted. The sorted results make this a useful method for ordered or time-series data

* joins - on - left_on, right_on
* type of join - how - inner, outer , left, right
* default order - outer
* Supports suffixes
* calling function - pd.merge_ordered(df1,df2)

## Forward fill
pd.merge_ordered(df1, df2, on="column", suffixes=("_df1","_df2"), fill_method="ffill")

## merge.asof()
similar to merge_ordered
match on nearest key not exact match
Merged "on" column must be sorted

pd.merge_asof(df1,df2, on="column",suffixes=("_df1","_df2"))

With direction
pd.merge_asof(df1,df2, on="column",suffixes=("_df1","_df2"),direction="forward")
directions can also be "backwards" and "nearest"

## Selecting data using .query()

Accepts input string - used to determine what rows are returned

df.query("column >= 100")
df.query("column1 > 100 and column2<100")
df.query("column1 > 100 or column2<100")

df.query('column1=="text" or (column1=="text" and column2 =90)')

## Reshaping data with .melt()

To convert wide talbes to long tables

df = df.melt(id_vars = ['column1','column2'])

use value vars to control which data is displayed
df = df.melt(id_vars = ['column1','column2'],value_vars=['attribute','attribute'])

changing column names

df = df.melt(id_vars = ['column1','column2'],value_vars=['attribute','attribute'],var_name=['year'],value_name='dollars')

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

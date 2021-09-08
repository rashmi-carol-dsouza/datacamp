# Inner Join

df_merge = df.merge(df2, on="common column")

To control suffix
df_merge = df.merge(df2, on="common column",suffixes=('_df','_df2'))

df_merge = df.merge(df2, on="common column", how="inner")

## Merging using two columns

df_merge = df.merge(df2, on=["column1",'column2'])


## Merging more than one table

df_merge = df.merge(df2, on="common column") \ .merge(df3, on="comon column")

## Left Joint

A left join returns all rows of data from the left table and only those rows from the right table where key columns match.

df_merge = df.merge(df2, on = 'common column', how="left")

## Other joins
# Types of data

Text data 
Integers
Decimals
Binary - Yes or no
Dates
Categories -  Marriage Status, gender 

Str
int
float
bool
datetime
category


## How to check data types per column?

dataframe.info()

## How to find summary statistic of a single column

print(df['column of interest'].describe())

## How to remove a character from a string?

df["Column name"] = df["Column name"].str.strip("char to remove")

## How to convert data type?

df["Column name"] = df["Column name"].astype("data type to convert to")

## How to verify if the data type has been converted?

assert df["Column name"].dtype == "Converted data type"

# Data Range Constraints

## How to set the date as current date

import datetime as dt
today_date = dt.date.today()

## How to sort data by date

df[df["column"] > dt.date.today()]

## How to deal with out of range data

1. Drop it

Only drop data when a small set of data is affected by values

2. Setting custom minimums and maximums 

3. Treat data as missing or imputed

4. Setting custom values depending on business assumptions

## How to isolate outliers

df[df["column"] > value]

## How to drop outliers

df = df[df["column"] > value]

or 

df.drop(df[df["column"]> value].index,inplace=True)

To check it use
assert df["column"].max() <= value

To change values that are out of range
df.loc[df["column"] > value, "column"] = value 

## How to convert column to datetime
df["column"] = pd.to_datetime(df["column"])

## How to check if the conversion was sucessful

assert df["Column name"].dtype == "datetime64[ns]"

## How to find duplicates

duplicates = df.duplicated()

## How to find duplicated values

df[duplicates]

## How to find duplicated rows

column_names = ["c1","c2","c3"]
duplicates = df.duplicated(subset = column_names, keep = False)

df[duplicates].sort_values(by="column_name")

## How to treat duplicate values

same subset and keet argumets as the duplicated method

inplace argument can be used to directly drop row inside the df without creating new object

df.drop_duplicates(inplace=True)

## How to group by columns and produce statistical summaries

column_names = ["c1","c2","c3"]
summaries = {"c1":"max","c2":"mean"}
df = df.groupby(by = column_names).agg(summaries).reset_index()

## How to ensure aggregation is complete
re run duplication
duplicates = df.duplicated(subset=column_names,keep=False)
df[duplicates].sort_values(by="c1")

## Membership constraints

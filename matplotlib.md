import matplotlib.pyplot as plt

## To show plot

plt.show()

## Histogram

df["Column_name"].hist()
To adjust the number of bars
df["Column_name"].hist(bins=5)

Layering plots 
df[df['sex'] == 'F'][height].hist()
df[df['sex'] == 'M'][height].hist()
for labelling colors
plt.label(["F","M"])
To make bars transparent
add argument .hist(alpha=0.7) 1 is solid color and 0 is white

## Bar plot

Bar plots can reveal relationships between a categorical variable and a numeric variable
ex for heights and sex
average_height_by_sex = df.groupby("sex")['height'].mean()
average_height_by_sex.plot(kind="bar",title="Mean height by sex")

## Line Plot
df.plot(x="column1",y='column2',kind='line')
rotating axis label
use argument rot=50 ie angle of ratation required

## Scatter Plot
df.plot(x="column1",y='column2',kind='scatter')


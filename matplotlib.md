import matplotlib.pyplot as plt

## Ploting

fig,ax = plt.subplots()
ax.plot(df["column1"],df['column2'])
ax.plot(df2["column1"],df2['column2'])

* To show plot

plt.show()

* Adding markers

ax.plot(df["column1"],df['column2'],marker="o")

o for circles
v for downward facing triangles

* Changing line styles

ax.plot(df["column1"],df['column2'],marker="o",linestyle="--")

use argument 'none' for no line

* To change color

ax.plot(df["column1"],df['column2'],marker="o",linestyle="--",color='r')

* To customize axes lables

ax.set_xlabel("Label")
ax.set_ylabel("Label")

* To add title

ax.set_title("Title")

## Small multiples with plt.subplots

fig,ax = plt.subplots()
fig,ax = plt.subplots(3,2)


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


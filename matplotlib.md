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

(row,column)

ax[0].plot(df["column1"],df['column2'])

* To standardize sub plots

fig,ax = plt.subplots(3,2, sharey=True)

## Plotting time-series data

fig,ax = plt.subplots()
ax.plot(df.index,df['column'])

* Zooming in on a decade
sixties = df["start date" : "end date"]
ax.plot(sixties.index,sixties['column'])

* Zooming in on one year
sixty_one = df["start date" : "end date"]
ax.plot(sixty_one.index,sixty_one['column'])

* use parse_dates argument - for converting a sequence of string columns to an array of datetime instances

## Plotting two time-series together

fig,ax = plt.subplots()
ax.plot(df.index,df['column'])
ax.plot(df2.index,df2['column'])

* Creating a twin of axes
ax2 = ax.twinx()

example
fig,ax = plt.subplots()
ax.plot(df.index,df['column'],color="red")
ax.set_xlabel("Label")
ax.set_ylabel("Label",color="red")
ax.tick_params("y", colors="red")
ax2 = ax.twinx()
ax.plot(df2.index,df2['column'],color="blue")
ax2.set_ylabel("Label",color="blue")
ax.tick_params("y", colors="blue")
plt.show()

* A function that plots time-series
def plot_timeseries(axes,x,y,color,xlabel,ylabel):
    axes.plot(x,y,color=color)
    axes.set_xlabel(xlabel)
    axes.set_ylabel(ylabel)
    axes.tick_params("y",colors=color)

- calling the function to plot a two time-series 

fig,ax=plt.subplots()
plot_timeseries(ax,df.index,df['column'],'red','Label','Label')
ax2 = ax.twinx()
plot_timeseries(ax,df.index,df['column'],'red','Label','Label')

## Annotating time series data

ax2.annotate("explanation", xy=(pd.Timestamp("date"),1))

- positioning the text

ax2.annotate("explanation", xy=(pd.Timestamp("date"),1),xytext=(pd.Timestamp("position-date"),-0.2))

- adding arrow between anotated text and text

ax2.annotate("explanation", xy=(pd.Timestamp("date"),1),xytext=(pd.Timestamp("position-date"),-0.2),arrowprops={})

- customising the arrow properties

ax2.annotate("explanation", xy=(pd.Timestamp("date"),1),xytext=(pd.Timestamp("position-date"),-0.2),arrowprops={'arrowstyle':'->','color':'gray'})

other customizations - https://matplotlib.org/users/annotations.html


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


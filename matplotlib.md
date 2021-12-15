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

# Quantitative Comparisions 

## Bar

fig,ax = plt.subplots()
ax.bar(df.index,df['column'])

* To fix labels incase of overlaping

ax.set_xticklables(df.index,rotation=90)

* Adding lables

ax.set_xlabel("Label")
ax.set_ylabel("Label")

* Creating a stacked bar chart

ax.bar(df.index,df['column'])
ax.bar(df.index,df['column2'],bottom=df['colomn1'])

* Creating a stack with three datas

ax.bar(df.index,df['column'])
ax.bar(df.index,df['column2'],bottom=df['colomn1'])
ax.bar(df.index,df['column3'],bottom=df['colomn1']+df['column2'])

* Adding a label
ax.bar(df.index,df['column'],label = 'label1')
ax.bar(df.index,df['column2'],bottom=df['colomn1'],label = 'label2')
ax.bar(df.index,df['column3'],bottom=df['colomn1']+df['column2'],label = 'label3')
ax.legend()

## Histogram

fig,ax = plt.subplots()
ax.hist(df["column"])
ax.hist(df2['column'])
ax.set_xlabel("Label")
ax.set_ylabel("Label")
plt.show()

* Labels are required

ax.hist(df["column"], label="Label")

- add legend

ax.legend()

* Setting number of bins

ax.hist(df["column"], label="Label", bins=4)

* Setting boundaries

ax.hist(df["column"], label="Label",bins=[100,200,300,etc])

* Adjusting transparency

ax.hist(df["column"], label="Label",bins=[100,200,300,etc], histtype="step")


## Statistical plotting

* Adding error bars to bar charts

ax.bar("Label",df['column'].mean(),yerr=df['column'].std())

* Adding error bars to a line plot

fig,ax = plt.subplots()
ax.errorbar(df['column1'],df["column2"],yerr=df["column-std-dev"])

* Adding box plots 
fig,ax = plt.subplots()
ax.boxplot([df["column"],df2['column']])
ax.set_xticklabels(["label1","label2"])

## Quantative comparision - scatter plots

fig,ax=plt.subplots()
ax.scatter(df["column1"],df["column2"])

* Customizing scatter plots

eighties = df["start_date":"end_date"]
nineties = df["start_date":"end_date"]
fig,ax=plt.subplots()
ax.scatter(eighties["column1"],eighties["column2"],color="blue",label="eighties")
ax.scatter(nineties["column1"],nineties["column2"],color="red",label="nineties")
ax.legend()

* Encoding a third variable by colour

fig,ax=plt.subplots()
ax.scatter(df["column1"],df["column2"],c=df.index)

## Preparing figures to share with others

## Changing plot styles

plt.style.use("ggplot")

* To go back to default style

plt.style.use("default")

More examples - https://matplotlib.org/2.0.2/gallery.html#style_sheets

* General Guidelines

Dont use dark backgrounds. You can use colorblind friendly style if colors are important. 
Avoid colored background if you will print the visualization to use less ink. If printed is b&w, use 'grayscale'

## Saving your visualizations

last line of code - fig.savefig("df.png")

Other formats 

- jpg - good choice if image is to be used for website or other uploads

- svg - good choice if image is to be edited later in another photo editing software

* To control file size (quality = 1 to 100)
fig.savefig("df.jpg", quality=50)
fig.savefig("df.jpg", dpi=300)

* Controlling figure size (Width,height)

fig.set_size_inches([5,3])


* Checking files in directory

ls

## Automating figures from data

fig,ax = plt.subplots()

for attribute in column:
    column_df = df[df["column"] == attribute]
    ax.bar(attribute,column_df['column'].mean(),yerr=column_df['column'].std())


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


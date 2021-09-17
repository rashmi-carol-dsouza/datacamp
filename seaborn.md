import seaborn as sns
import matplotlib.pyplot as plt

## Scatter plot

sns.scatterplot(x=column1/list1,y-column2/list2)
plt.show()

## Count plot 

sns.countplot(x=column/list)

* using dataframe with countplot()
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("df.csv")
sns.countplot(x="column",data=df)
plt.show()

## Adding a third variable with hue

import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns

df = sns.load_dataset("df")
sns.scatterplot(x="column1",y="column2",data=df,hue="attribute",hue_order["Yes","No"])
plt.show()

or 

hue_colors={"Yes":"red","No":"black"}
sns.scatterplot(x="column1",y="column2",data=df,hue="attrubute",palette=hue_colors)
plt.show()

* Using hue with count plots 

sns.countplot(x="column1",data=df,hue="attribute")

## Relational plots and subplots

* relplot()


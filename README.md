# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
/* 
Name : O. Shanthan Kumar Reddy
Register Number : 212220040107
**Data Visualization - Iris.csv**
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
df = pd.read_csv("/content/Iris.csv")
df.head()
df.info()
df["Species"].value_counts()
sns.countplot(x='Species', data=df, )
plt.show()
sns.scatterplot(x='SepalLengthCm', y='SepalWidthCm',
                hue='Species', data=df, )
plt.legend(bbox_to_anchor=(1, 1), loc=2)
plt.show()
sns.scatterplot(x='PetalLengthCm', y='PetalWidthCm',
                hue='Species', data=df, )
plt.legend(bbox_to_anchor=(1, 1), loc=2) 
plt.show()
sns.pairplot(df.drop(['Id'], axis = 1), hue='Species', height=2)
fig, axes = plt.subplots(2, 2, figsize=(10,10)) 
axes[0,0].set_title("Sepal Length")
axes[0,0].hist(df['SepalLengthCm'], bins=7)
axes[0,1].set_title("Sepal Width")
axes[0,1].hist(df['SepalWidthCm'], bins=5); 
axes[1,0].set_title("Petal Length")
axes[1,0].hist(df['PetalLengthCm'], bins=6); 
axes[1,1].set_title("Petal Width")
axes[1,1].hist(df['PetalWidthCm'], bins=6);
sns.heatmap(df.corr(method='pearson').drop(
    ['Id'], axis=1).drop(['Id'], axis=0),
            annot = True); 
plt.show()
*/
```
# OUPUT
## Data Visualization - Iris.csv
![Data_Visualization](/images/img.png)
![Data_Visualization](/images/img2.png)
![Data_Visualization](/images/img3.png)
![Data_Visualization](/images/img4.png)
![Data_Visualization](/images/img5.png)
![Data_Visualization](/images/img6.png)

# RESULT
Thus the Data Visualization for the given dataset had been executed successfully.

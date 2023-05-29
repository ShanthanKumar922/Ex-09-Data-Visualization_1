# Ex-09-Data-Visualization_1

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
Program developed by:
Name: O. Shanthan Kumar Reddy
Reg no: 212220040107


#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df

#removing unnecessary data variables
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df

df.isnull().sum()

#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()

#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()

#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()

#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()

#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')

#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()

#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')

#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)

#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])

#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()

#HeatMap
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()

```

# OUTPUT

### Initial Dataset:


### Cleaned Dataset:

<img width="541" alt="t" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/2d9e2b01-2572-4e5b-b205-d8eb88e08145">

<img width="118" alt="t1" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/b06c38ee-587a-4e6c-baf2-8ba1425b350c">

### Removing Outliers:

<img width="449" alt="t2" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/79c9b75d-7e47-41c1-95d0-e63e349d56f4">

<img width="451" alt="t3" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/203ca065-1031-427f-bda6-b34455a912f8">

### Line PLot:

<img width="224" alt="t4" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/a3e3b47b-4cb7-4af6-88b2-3aabba564f9f">

<img width="224" alt="t5" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/3aa0f534-3277-4b3e-a879-282f75f83a50">

<img width="224" alt="t6" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/a14f191e-2782-46f7-a4bc-8e75a997f351">

<img width="223" alt="t7" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/16b455ad-474f-431c-ae2f-434f7dbbd24c">

<img width="224" alt="t8" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/5c1ca27f-1f50-4279-a76f-b84d657e8e63">

<img width="538" alt="t9" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/d2292b2a-3751-4862-9d5d-8855ffc537e2">

### Bar Plots:

<img width="224" alt="t10" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/ea9e2528-5755-47b0-95f8-37621ebd5c58">

<img width="224" alt="t11" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/77c1e7e1-273f-428e-9e21-a4dbf665890e">

<img width="226" alt="t12" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/5a67f622-a8ff-42f1-96a3-3ec11bc4f618">

<img width="452" alt="t13" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/efe1f2a7-c2fb-4a1e-8e20-1d339f924c4a">

<img width="536" alt="t14" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/8228833e-6d4b-4c64-abfe-e95577a73896">

### Histograms:

<img width="223" alt="t15" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/50d67ed5-79f4-4829-af1b-6a941089520b">

<img width="227" alt="t27" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/de6609d3-48d8-4251-acf1-8fc2f0a5942f">

<img width="224" alt="t28" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/e8a1c666-2ecb-41e4-a6b9-4a3f5dfa102e">

<img width="223" alt="t29" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/a31e3a50-1b61-44c3-b3af-d77ee60e7a88">

<img width="224" alt="t30" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/923ef5f1-2bfd-40ca-87ed-16e21b23509f">

### Count plots:

<img width="224" alt="t16" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/f108a2ac-3117-465b-a753-d99c1f9350eb">

<img width="223" alt="t17" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/31a9c157-d0ed-47d7-9a4f-8145544254c1">

<img width="375" alt="t31" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/4a81ff65-de4b-459e-9e33-0c2b70db9b0d">

<img width="229" alt="t32" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/e7ca88d9-7995-4e02-9e0f-1793c697fc7e">

<img width="221" alt="t33" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/8127680a-760d-44e3-a33d-4acbdf79e5de">


### Bar Charts:

<img width="376" alt="t18" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/1746847c-9bed-4e6d-80fb-acc370250bad">

<img width="223" alt="t19" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/d8599d46-df0b-4550-a924-a158c54ea99a">

<img width="374" alt="t20" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/0d60a021-d287-4cf3-acbc-3be246fd1605">

<img width="527" alt="t21" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/9c8433e8-d853-498f-b220-c6c20ebf7286">

<img width="227" alt="t34" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/85af9d2a-3435-4eb4-a015-3e70e4def231">

<img width="224" alt="t35" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/584243d1-50a9-42e0-9f08-d2691c5d9021">

<img width="226" alt="t36" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/165955ca-108a-428b-9c0b-99434d969a7e">

### KDE Plots:

<img width="225" alt="t22" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/32970153-e7f7-45cd-9abd-0ad366a82a9a">

<img width="227" alt="t23" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/4feb747b-0c3c-40d8-918d-14b225f7c908">

### Violin Plot:

<img width="221" alt="t24" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/f8e722ab-4360-41d6-8333-2e35316ef096">

### Point Plots:

<img width="227" alt="t25" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/9dee2516-7f28-499b-9efe-09e37782d42c">

<img width="227" alt="t26" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/f7b93efe-2bb6-48d6-8a27-7e2c0babc8bc">

### Pie Charts:

<img width="335" alt="t37" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/a39ed945-2150-476d-a9f0-7b4fa52dfffb">

<img width="367" alt="t38" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/35b4f145-42ea-412c-b419-ad8073c32d30">

<img width="223" alt="t39" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/e9f9c5f6-7ef8-40a5-b17a-4ca9ebe29852">

<img width="378" alt="t40" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/6ba2b726-60a2-4c73-8426-0eec890ae118">

<img width="308" alt="t41" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/e237001f-98b7-4bc4-90ab-18e75509710c">

<img width="197" alt="t42" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/90433c03-ab52-44c2-8be2-0c87dd5a5de6">


### HeatMap:

<img width="368" alt="t43" src="https://github.com/ShanthanKumar922/Ex-09-Data-Visualization_1/assets/127843136/7281ff58-e4ea-4ce3-a54d-b950ca9e1f6e">


### Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file





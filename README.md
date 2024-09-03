# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
## Data Cleaning
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df

```
![image](https://github.com/user-attachments/assets/be44f804-7c82-4a93-afa5-582d4250d745)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/3bff74bb-5901-478f-8684-9b385e47c784)

```
df.isnull().any()
```
![image](https://github.com/user-attachments/assets/1b5560d1-a783-4c21-be91-85e2e6d29249)

```
df.dropna()
```
![image](https://github.com/user-attachments/assets/836fbeba-0078-4e45-9c16-703e2b5e8394)

```
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/f4a465f2-00af-48db-ae9d-c35a2faf5642)

```
df.fillna(method = "ffill")
```
![image](https://github.com/user-attachments/assets/19acf483-a3c0-4b42-99e1-d32354d80009)

```
df.fillna(method = 'bfill')
```
![image](https://github.com/user-attachments/assets/1a47f45e-ee36-42fc-b07c-e3c6696e1698)

```
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/user-attachments/assets/b652d24a-1d82-419b-936e-af90bae7913e)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/user-attachments/assets/27eb1007-0cc9-47da-90a5-e99f2831c6a6)

## IQR(Inter Quartile Range)
```
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/user-attachments/assets/c162b71a-1b85-4e46-a145-78c744573190)

```
ir.describe()
```
![image](https://github.com/user-attachments/assets/a8b6baff-5da2-4a81-959c-8bc688a6dc26)

```
import seaborn as sns
import matplotlib.pyplot as plt
sns.boxplot(x='sepal_width',data=ir)
plt.show()

```
![image](https://github.com/user-attachments/assets/0b10748d-c60e-4b1a-b5a2-ef5cf76f4afb)

```
 c1=ir.sepal_width.quantile(0.25)
 c3=ir.sepal_width.quantile(0.75)
 iq=c3-c1
 print(c3)
```
![image](https://github.com/user-attachments/assets/5eefc5a4-4171-4ac2-af05-5e0ea8d3d8ff)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/user-attachments/assets/23d550cc-559d-4c98-862c-7803584d116b)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/user-attachments/assets/b64fdcc3-808c-49bc-912f-b3dda38ada12)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/user-attachments/assets/8c3f9b78-49ff-4762-966d-08469f492f62)

## Z - Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/user-attachments/assets/1057cb26-c51d-4f0f-af15-6f843466d941)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/b952eda4-58c7-4483-a037-2f79d23fc7fa)

```
low = q1- 1.5*iqr
low
```
![image](https://github.com/user-attachments/assets/2846b1c3-b249-4ca3-8ecb-f4855aaaeb8f)

```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/user-attachments/assets/5be1bfa3-7fb7-4d8d-8550-dfb66ace0109)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/user-attachments/assets/0efb9e7b-bd23-4e9f-88d8-7d51358e47e3)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/user-attachments/assets/bb8c6a93-79f4-4c6d-9ab5-3cd8b3c336f4)

```
df1 = df[z<3]
df1
```
![image](https://github.com/user-attachments/assets/b6da7bf0-939f-4a4a-a04b-8c80d0b423d6)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.

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
![D1](https://github.com/user-attachments/assets/2788ce7b-594f-4de1-929d-6da1bb66feb7)

```
df.isnull().sum()
```
![D2](https://github.com/user-attachments/assets/bada091f-fbc8-46f7-a70b-f146d81a9e8c)

```
df.isnull().any()
```
![D3](https://github.com/user-attachments/assets/1db72edd-9eb9-47f3-b9f7-12edb813ac88)

```
df.dropna()
```
![D4](https://github.com/user-attachments/assets/88fe9d9a-3a4f-466e-972c-182ac3626054)

```
df.fillna(0)
```
![D5](https://github.com/user-attachments/assets/3b12b148-508c-4e47-b5a7-ef1130e4b66b)

```
df.fillna(method = "ffill")
```
![D6](https://github.com/user-attachments/assets/e17fce7e-8054-4b11-bb04-0e17b2b3016c)

```
df.fillna(method = 'bfill')
```
![D7](https://github.com/user-attachments/assets/48c82c46-c62e-4556-96a0-1f7498b74abf)

```
df_dropped = df.dropna()
df_dropped
```
![D8](https://github.com/user-attachments/assets/4f762cf5-31c0-4104-b65b-e3ace87836ec)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![D9](https://github.com/user-attachments/assets/dc6d79f9-5324-458e-9b8b-4e2a739e6bc6)

## IQR(Inter Quartile Range)
```
ir=pd.read_csv('iris.csv')
ir
```
![I1](https://github.com/user-attachments/assets/5b465543-1470-496c-b7fb-d57895bf73e5)

```
ir.describe()
```
![I2](https://github.com/user-attachments/assets/728264b3-1d5f-4db5-aad2-301db04fb5fd)

```
import seaborn as sns
import matplotlib.pyplot as plt
sns.boxplot(x='sepal_width',data=ir)
plt.show()

```
![I3](https://github.com/user-attachments/assets/de0ad3b4-58dd-4a56-b3c2-c480f387b0ad)

```
 c1=ir.sepal_width.quantile(0.25)
 c3=ir.sepal_width.quantile(0.75)
 iq=c3-c1
 print(c3)
```
![I4](https://github.com/user-attachments/assets/6dc14587-f63c-4114-bfb8-d915c05fc46c)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![I5](https://github.com/user-attachments/assets/e6e3599e-9b3f-40cc-b8fa-b4074959220c)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![I6](https://github.com/user-attachments/assets/44c34a59-6696-41f1-bb72-78cd3539fa4e)

```
sns.boxplot(x='sepal_width',data=delid)
```
![I7](https://github.com/user-attachments/assets/1390de71-84a9-4f50-83b1-4047983e3bda)

## Z - Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![Z1](https://github.com/user-attachments/assets/8a7b2811-79b4-4f9e-a666-d0a5293a4c2a)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![Z2](https://github.com/user-attachments/assets/efa9ada9-f9b0-4a41-b2c7-c2bf3199c23f)

```
low = q1- 1.5*iqr
low
```
![output](./Outputs/Z3.png)
![Z3](https://github.com/user-attachments/assets/3d5800fc-b6d2-4b3c-95a0-cc273f47ae00)

```
high = q3 + 1.5*iqr
high
```
![Z4](https://github.com/user-attachments/assets/cb1e7051-13f5-44ce-ad7f-4845cd542584)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![Z5](https://github.com/user-attachments/assets/763e56df-e506-47ec-bf87-4ddf1a3a4766)

```
z = np.abs(stats.zscore(df['height']))
z
```
![Z6](https://github.com/user-attachments/assets/545fe736-2fa8-4219-8056-7cfb05f16c15)

```
df1 = df[z<3]
df1
```
![Z7](https://github.com/user-attachments/assets/2e2c162c-9af4-4ac9-a573-3f2dbd88004c)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.

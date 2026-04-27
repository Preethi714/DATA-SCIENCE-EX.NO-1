# EX.NO:1  Data Cleaning Process

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
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
df = pd.read_csv('D:/Loan_data.csv')
df.head()

# Handling Missing Values
df.isnull()
df.isnull().sum()

# Fill Missing Values with 0
df_fill_0 = df.fillna(0)
df_fill_0

# Forward Fill
df_ffill = df.ffill()
df_ffill

# Backward Fill
df_bfill = df.bfill()
df_bfill

# Drop Missing Values
df_dropna = df.dropna()
df_dropna

# Save Cleaned Data
df_dropna.to_csv('clean_data.csv', index=False)

## OUTLIER DETECTION
# IQR Method (Using Iris Dataset)
ir = pd.read_csv('D:/iris.csv')
ir.head()

# Boxplot for Outlier Detection
sns.boxplot(x=ir['sepal_width'])
plt.show()

# Calculate IQR
Q1 = ir['sepal_width'].quantile(0.25)
Q3 = ir['sepal_width'].quantile(0.75)
IQR = Q3 - Q1
print("IQR:", IQR)

# Detect Outliers
outliers_iqr = ir[
    (ir['sepal_width'] < (Q1 - 1.5 * IQR)) |
    (ir['sepal_width'] > (Q3 + 1.5 * IQR))
]
outliers_iqr

# Remove Outliers
ir_cleaned = ir[
    ~((ir['sepal_width'] < (Q1 - 1.5 * IQR)) |
      (ir['sepal_width'] > (Q3 + 1.5 * IQR)))
]
ir_cleaned

# Z-Score Method
data = [1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,
        54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df_z = pd.DataFrame(data, columns=['values'])
df_z

# Calculate Z-Scores
z_scores = np.abs(stats.zscore(df_z))
z_scores

# Detect Outliers
threshold = 3
outliers_z = df_z[z_scores > threshold]
print("Outliers:")
outliers_z

# Remove Outliers
df_z_cleaned = df_z[z_scores <= threshold]
df_z_cleaned
```
<img width="1240" height="490" alt="Screenshot 2026-03-17 101306" src="https://github.com/user-attachments/assets/6378cc44-09a8-430a-9ecb-69d067a44221" />

<img width="92" height="825" alt="image" src="https://github.com/user-attachments/assets/7170b332-d964-4cdb-bd7a-e8e360e10709" />

# Result
Thus, the given data and perform data cleaning and save the cleaned data to a file is succesfully completed.

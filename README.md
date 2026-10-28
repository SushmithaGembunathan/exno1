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
```
import pandas as pd
import numpy as np

df = pd.read_csv("Data_set.csv")

print("\nOriginal Data:\n", df.head(10))
print("\nMissing values:\n", df.isnull().sum())

clean = df.copy()

for col in clean.select_dtypes(include="number").columns:
    clean[col] = clean[col].fillna(clean[col].median())

for col in clean.select_dtypes(include="object").columns:
    if not clean[col].mode().empty:
        clean[col] = clean[col].fillna(clean[col].mode()[0])

print("\nMissing values after cleaning:\n", clean.isnull().sum())
print("\nCleaned Data:\n", clean.head(10))

clean.to_csv("Data_set_cleaned.csv", index=False)
print("\nSaved Data_set_cleaned.csv")
```
### Output :
<img width="983" height="1065" alt="image" src="https://github.com/user-attachments/assets/57e50c0f-9b7e-475c-b771-f9ef4b2c61d3" />

<img width="737" height="1078" alt="image" src="https://github.com/user-attachments/assets/dc5d74e1-ea73-4f21-9214-a88f397d3c35" />

```
import pandas as pd
import numpy as np

df = pd.read_csv("SAMPLEIDS.csv")

print("\nOriginal Data:\n", df.head(10))
print("\nDuplicate rows:", df.duplicated().sum())

clean = df.drop_duplicates().copy()
for col in clean.select_dtypes(include="object").columns:
    clean[col] = clean[col].str.strip()
    print("\nUnique values in", col)
    print(clean[col].unique())

print("\nDuplicate rows after removal:", clean.duplicated().sum())
print("\nCleaned Data:\n", clean.head(10))

clean.to_csv("SAMPLEIDS_cleaned.csv", index=False)
print("\nSaved SAMPLEIDS_cleaned.csv")
```
### Output :
<img width="967" height="1072" alt="image" src="https://github.com/user-attachments/assets/95f14af4-88e0-44c0-b1da-d60d7f91ef0e" />

```
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

df = pd.read_csv("heights.csv")

print("\nOriginal Data:\n", df.head(10))

for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR results for", col)
    print("Lower limit:", lower)
    print("Upper limit:", upper)
    print("Unusual measurements:\n", outliers)

for col in df.select_dtypes(include="number").columns:
    plt.figure()
    plt.boxplot(df[col].dropna())
    plt.title("Unusual measurements in " + col)
    plt.ylabel(col)
    plt.show()
```
### output :
<img width="705" height="995" alt="image" src="https://github.com/user-attachments/assets/7715220b-f896-4a44-a730-e863c7628f44" />

```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("iris.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
### output :
<img width="677" height="843" alt="image" src="https://github.com/user-attachments/assets/15a6f21b-2ba8-4c04-a106-12b1049bc126" />

```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv("Loan_data.csv")

print("\nOriginal Data:\n", df.head(10))


for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if values.empty:
        continue

    q1 = values.quantile(0.25)
    q3 = values.quantile(0.75)
    iqr = q3 - q1

    lower = q1 - 1.5 * iqr
    upper = q3 + 1.5 * iqr

    outliers = values[(values < lower) | (values > upper)]

    print("\nIQR outliers in", col)
    print(outliers if not outliers.empty else "None")

# STEP 3: Z-SCORE OUTLIER DETECTION
for col in df.select_dtypes(include="number").columns:

    values = df[col].dropna()

    if len(values) < 2:
        continue

    z = np.abs(stats.zscore(values))
    outliers = values[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers if not outliers.empty else "None")
```
### output :
<img width="797" height="1056" alt="image" src="https://github.com/user-attachments/assets/0a6a8a5b-6385-4bbf-8198-5214ea229ad7" />

<img width="912" height="1078" alt="image" src="https://github.com/user-attachments/assets/39eed437-7d10-4c99-a928-fd27d07cd62c" />

<img width="783" height="1078" alt="image" src="https://github.com/user-attachments/assets/2d2bbd3c-8cb8-4938-a945-73970359f98b" />

<img width="861" height="1078" alt="image" src="https://github.com/user-attachments/assets/50d190e6-ccb1-4718-80c9-aee76b058015" />



# Result
The datasets are inspected and cleaned by handling missing values and duplicates. Potential outliers are detected using the IQR method, visualized with boxplots, and removed. The processed datasets and outlier reports are saved for further analysis.

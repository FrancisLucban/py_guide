# 🛠️ Pandas Boilerplates (Expanded)

```py
import pandas as pd
import numpy as np
```

## 🔹 Initialize a DataFrame

```py
# From dictionary
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [25, 30, 35],
    "Salary": [50000, 60000, 70000]
}
df = pd.DataFrame(data)

# From list of lists
df2 = pd.DataFrame(
    [[1, "A"], [2, "B"], [3, "C"]],
    columns=["ID", "Label"]
)

# From NumPy array
arr = np.arange(9).reshape(3,3)
df3 = pd.DataFrame(arr, columns=["Col1","Col2","Col3"])

# From CSV
df_csv = pd.read_csv("data.csv")

🔹 Inspect Data
df.head()        # first 5 rows
df.tail()        # last 5 rows
df.info()        # summary of columns, dtypes, nulls
df.describe()    # stats summary (numerical cols)
df.shape         # rows, columns
df.columns       # list of column names
df.dtypes        # data types of each column
```

## 🔹 Cleaning Data

```py
# Drop missing values
df.dropna(inplace=True)

# Fill missing values
df.fillna(0, inplace=True)                  # replace with 0
df['Age'].fillna(df['Age'].mean(), inplace=True)  # replace with mean

# Rename columns
df.rename(columns={"Name":"FullName"}, inplace=True)

# Drop column(s)
df.drop(columns=["Salary"], inplace=True)

# Drop row(s) by index
df.drop(index=[0,1], inplace=True)

# Remove duplicates
df.drop_duplicates(inplace=True)

# Change data type
df['Age'] = df['Age'].astype(int)

# Replace values
df['Name'].replace({"Alice":"Alicia"}, inplace=True)

# String cleanup
df['Name'] = df['Name'].str.strip().str.lower()

# Reset index
df.reset_index(drop=True, inplace=True)
```

# 🔹 Useful Data Checks

```py
df.isnull().sum()      # count of nulls per column
df.duplicated().sum()  # count duplicates
df['Age'].unique()     # unique values
df['Age'].nunique()    # number of unique values
df['Age'].value_counts()  # frequency counts
```
# 📊 Data Science & Analysis with Python

## 1. 🧾 Basic Concepts

- **Data Science:** Extracting insights from raw data using statistics, programming, and visualization.
- **Data Analysis:** Cleaning, exploring, and interpreting data.
- **Data Visualization:** Graphically representing data for understanding and decision-making.

**Core Libraries:**

- `numpy` → numerical computations (arrays, math ops).
- `pandas` → data manipulation (tables, series, cleaning).
- `matplotlib` → base plotting.
- `seaborn` → statistical plots (built on matplotlib).

## 2. 🔢 NumPy (Numerical Computing)

```py
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
zeros = np.zeros((2,3))
ones = np.ones((3,3))
rand = np.random.rand(2,2)

# Array operations
arr.mean()        # average
arr.std()         # standard deviation
arr.sum()         # sum
arr.reshape(5,1)  # reshape
```

## 3. 📑 Pandas (Data Manipulation)

```py
import pandas as pd

# Load data
df = pd.read_csv("data.csv")
df.head()      # first 5 rows
df.info()      # data summary
df.describe()  # stats summary

# Selecting
df['column']
df[['col1','col2']]
df.iloc[0:5]   # by index

# Filtering
df[df['age'] > 30]
df[(df['age'] > 30) & (df['gender'] == 'M')]

# Cleaning
df.dropna()                 # remove missing
df.fillna(0)                # replace missing
df.rename(columns={'old':'new'}, inplace=True)

# Grouping
df.groupby('category')['value'].mean()

# Sorting
df.sort_values('age', ascending=False)

# Save
df.to_csv("cleaned.csv", index=False)
```

## 4. 📈 Matplotlib (Visualization Basics)

```py
import matplotlib.pyplot as plt

x = [1,2,3,4,5]
y = [2,4,6,8,10]

# Basic plot
plt.plot(x, y, marker='o')
plt.title("Line Plot")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.show()

# Bar chart
plt.bar(['A','B','C'], [10,20,15])

# Histogram
plt.hist([1,2,2,3,3,3,4,4,5], bins=5)
```
> [!NOTE]
> [MORE MATPLOTLIB INFO HERE](datascience_additional/matplotlib_more.md)


## 5. 🎨 Seaborn (Statistical Visualization)

```py
import seaborn as sns

# Load example dataset
tips = sns.load_dataset("tips")

# Scatterplot
sns.scatterplot(x="total_bill", y="tip", data=tips)

# Histogram / KDE
sns.histplot(tips["total_bill"], bins=20, kde=True)

# Boxplot
sns.boxplot(x="day", y="total_bill", data=tips)

# Heatmap (correlation matrix)
corr = tips.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap="coolwarm")
```

## 6. 🔍 Data Analysis Workflow

1. Import libraries + dataset.
2. Explore (.head(), .info(), .describe()).
3. Clean (missing values, rename cols, handle outliers).
4. Analyze (grouping, filtering, aggregations).
5. Visualize (trends, distributions, correlations).
6. Report/Save results.

## 7. 🛠️ Useful Boilerplates

```py
# Check missing values
df.isnull().sum()

# Unique values
df['column'].unique()

# Value counts
df['column'].value_counts()

# Apply function
df['new_col'] = df['col'].apply(lambda x: x*2)

# Merge / Join
merged = pd.merge(df1, df2, on="id", how="inner")

# Pivot table
pd.pivot_table(df, values="sales", index="region", columns="year", aggfunc="sum")
```
> [!NOTE]
> [MORE USEFUL BOILERPLATES HERE](datascience_additional/boilerplates_more.md)

## 📊 Sample Practical Pipeline 

**data.csv**

```py
# Example dictionary to simulate CSV contents
data = {
    "id": [1, 2, 3, 4, 5],
    "name": ["Alice", "Bob", "Charlie", "David", "Eva"],
    "age": [25, 30, None, 40, 29],                 # notice missing value
    "gender": ["F", "M", "M", "M", "F"],
    "city": ["New York", "Los Angeles", None, "Chicago", "Houston"], # missing value
    "date": ["2023-01-05", "2023-02-12", "2023-03-20", "2023-04-10", "2023-05-01"],
    "category": ["Electronics", "Clothing", "Electronics", "Sports", "Clothing"],
    "quantity": [1, 2, 3, 4, 2],
    "price": [500, 40, 200, 100, 60],
    "amount": [500, 80, 600, 400, -50],            # notice invalid negative
    "target": [1, 0, 1, 0, 1]                      # example label for ML
}
```

---

```py
# 0. imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load / initialize dataframe
df = pd.read_csv("data.csv")             # read CSV into a DataFrame

# 2. Quick peek (sanity check)
df.head()                                # first rows
df.sample(5)                              # random sample
df.shape                                  # (rows, cols)
df.info()                                 # dtypes & null counts
df.describe()                             # summary statistics for numeric cols

# 3. Find missing values
df.isnull().sum()                         # count nulls per column

# 4. Handle missing values (choose strategy)
df['age'].fillna(df['age'].median(), inplace=True)  # numeric inputation
df['city'].fillna("Unknown", inplace=True)          # categorical fill
df.dropna(subset=['essential_col'], inplace=True)   # drop rows missing essential data

# 5. Remove duplicates & invalid rows
df.drop_duplicates(inplace=True)
df = df[df['amount'] >= 0]                # filter out invalid negatives (example)

# 6. Fix types & parse dates
df['date'] = pd.to_datetime(df['date'], errors='coerce')
df['id'] = df['id'].astype(str)

# 7. Normalize / clean text columns
df.columns = df.columns.str.strip().str.lower()      # column name cleanup
df['name'] = df['name'].str.strip().str.title()      # string cleanup

# 8. Feature engineering (create useful columns)
df['month'] = df['date'].dt.month
df['total'] = df['quantity'] * df['price']

# 9. Encode categorical variables (for analysis or modeling)
df = pd.get_dummies(df, columns=['category'], drop_first=True)   # one-hot
# or
df['gender_code'] = df['gender'].map({'M':0, 'F':1})

# 10. Exploratory Data Analysis (EDA) — quick plots & checks
plt.figure(); plt.hist(df['total'].dropna(), bins=30); plt.title("Total distribution"); plt.show()
plt.figure(); sns.boxplot(x='category', y='total', data=df); plt.show()
plt.figure(); sns.scatterplot(x='quantity', y='total', data=df, alpha=0.6); plt.show()
corr = df.select_dtypes(include=[np.number]).corr()
plt.figure(figsize=(6,5)); sns.heatmap(corr, annot=True); plt.show()

# 11. Aggregation / group analysis
sales_by_month = df.groupby('month')['total'].sum().reset_index()
top_customers = df.groupby('customer_id')['total'].sum().nlargest(10)

# 12. Prepare for modeling (optional skeleton)
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

# example: simple supervised workflow if you have a target column "target"
X = df.drop(columns=['target', 'date'])            # features
y = df['target']                                   # label
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# scale numeric features (one approach)
num_cols = X_train.select_dtypes(include=[np.number]).columns
scaler = StandardScaler()
X_train[num_cols] = scaler.fit_transform(X_train[num_cols])
X_test[num_cols]  = scaler.transform(X_test[num_cols])

model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)
print("Test accuracy:", model.score(X_test, y_test))

# 13. Save cleaned dataset & results
df.to_csv("data_cleaned.csv", index=False)
sales_by_month.to_csv("sales_by_month.csv", index=False)
```

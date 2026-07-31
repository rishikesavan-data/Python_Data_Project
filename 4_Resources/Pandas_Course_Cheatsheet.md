# Pandas Cheat Sheet

---

# 1. Loading & Viewing Data

## Convert Polars to Pandas
```python
df = df["train"].to_pandas()
```

## First Rows
```python
df.head(5)
```

Output
| Name | Age |
|------|-----|
| John | 25 |
| Alex | 30 |

---

## Last Rows
```python
df.tail(5)
```

---

## Dataset Information
```python
df.info()
```

Shows:
- Number of rows
- Number of columns
- Data types
- Missing values
- Memory usage

---

## Statistical Summary
```python
df.describe()
```

Returns:

- Count
- Mean
- Std
- Min
- Quartiles
- Max

---

# 2. Dataset Properties

## Number of Rows & Columns
```python
df.shape
```

Output

```python
(1000, 5)
```

---

## Number of Rows
```python
len(df)
```

---

## Column Names
```python
df.columns
```

---

## Index
```python
df.index
```

---

## Index Name
```python
df.index.name
```

Assign a name:

```python
df.index.name = "Job_Index"
```

---

# 3. Accessing Data

## Single Column
```python
df["salary"]
```

---

## Multiple Columns
```python
df[["salary", "country"]]
```

---

## Row by Position
```python
df.iloc[0]
```

First row

---

## Multiple Rows
```python
df.iloc[0:5]
```

Rows 0–4

---

## Access by Label
```python
df.loc[0]
```

---

## Specific Rows & Columns
```python
df.loc[0:5, ["salary", "country"]]
```

---

# 4. Filtering Data

## Filter Rows

```python
df[df["salary"] > 50000]
```

---

## Multiple Conditions

```python
df[
    (df["salary"] > 50000)
    & (df["country"] == "USA")
]
```

---

## Missing Values

### Check Missing

```python
df.isna()
```

---

### Check Non-Missing

```python
df.notna()
```

---

# 5. Missing Value Handling

## Fill Missing Values

```python
df.fillna(0)
```

---

## Drop Missing Rows

```python
df.dropna()
```

---

# 6. Duplicate Handling

## Remove Duplicates

```python
df.drop_duplicates()
```

---

# 7. Sorting

## Sort by Column

```python
df.sort_values("salary")
```

Descending

```python
df.sort_values("salary", ascending=False)
```

---

## Sort by Index

```python
df.sort_index()
```

---

# 8. Row & Column Removal

## Drop Column

```python
df.drop(columns=["salary"])
```

---

## Drop Row

```python
df.drop(index=5)
```

---

# 9. Descriptive Statistics

## Count

```python
df["salary"].count()
```

Counts non-null values.

---

## Sum

```python
df["salary"].sum()
```

---

## Cumulative Sum

```python
df["sales"].cumsum()
```

Example

| Sales | Cumulative |
|-------|------------|
|100|100|
|200|300|
|150|450|

---

## Minimum

```python
df["salary"].min()
```

---

## Maximum

```python
df["salary"].max()
```

---

## Mean

```python
df["salary"].mean()
```

---

## Median

```python
df["salary"].median()
```

---

## Mode

```python
df["city"].mode()
```

Most frequent value.

---

## Row Index of Minimum Value

```python
df["salary"].idxmin()
```

---

## Row Index of Maximum Value

```python
df["salary"].idxmax()
```

---

## Unique Values

```python
df["country"].unique()
```

---

## Frequency Count

```python
df["country"].value_counts()
```

Example

| Country | Count |
|----------|------|
|USA|20|
|India|15|

---

# 10. Grouping

## Group By

```python
df.groupby("country")["salary"].mean()
```

Example

| Country | Avg Salary |
|----------|------------|
|India|45000|
|USA|75000|

---

# 11. Pivot Table

```python
df.pivot_table(
    values="salary",
    index="country",
    aggfunc="mean"
)
```

---

# 12. Date & Time

## Convert to Datetime

```python
df["date"] = pd.to_datetime(df["date"])
```

---

## Extract Month

```python
df["date"].dt.month
```

Output

```
1
2
3
```

---

## Format Month Name

```python
df["date"].dt.strftime("%b")
```

Output

```
Jan
Feb
Mar
```

---

# 13. Index Operations

## Set Index

```python
df.set_index("job_id")
```

---

## Reset Index

```python
df.reset_index()
```

---

# 14. Combining DataFrames

## Merge

```python
df1.merge(
    df2,
    on="customer_id",
    how="inner"
)
```

Types

- inner
- left
- right
- outer

---

## Concatenate

Stack rows

```python
pd.concat([df1, df2])
```

Stack columns

```python
pd.concat([df1, df2], axis=1)
```

---

# 15. Sampling & Copying

## Random Sample

```python
df.sample(5)
```

---

## Copy DataFrame

```python
df_copy = df.copy()
```

---

# 16. Apply Functions

## Apply

```python
df["salary"].apply(lambda x: x * 1.10)
```

Increase salary by 10%.

---

## Lambda Function

```python
lambda x: x + 10
```

Equivalent to

```python
def add(x):
    return x + 10
```

---

## Custom Function

```python
def categorize(age):
    if age >= 18:
        return "Adult"
    return "Child"

df["Category"] = df["Age"].apply(categorize)
```

---

# 17. Working with Lists

Suppose a column contains

```python
"[1,2,3]"
```

Convert string to list

```python
import ast

df["numbers"] = df["numbers"].apply(ast.literal_eval)
```

---

## Explode Lists

Before

| Name | Skills |
|------|---------|
|John|["SQL","Python"]|

```python
df.explode("Skills")
```

After

| Name | Skills |
|------|---------|
|John|SQL|
|John|Python|

---

# 18. Exporting Data

## Copy to Clipboard

```python
df.to_clipboard()
```

---

## Excel

```python
df.to_excel("data.xlsx")
```

---

## CSV

```python
df.to_csv("data.csv")
```

---

## Parquet

```python
df.to_parquet("data.parquet")
```

---

## Pickle

```python
df.to_pickle("data.pkl")
```

---

# 19. Visualization

## Bar Chart

```python
df["country"].value_counts().plot(kind="bar")
```

Creates a bar chart of frequency counts.

---

# 20. Common Workflow

```python
df = pd.read_csv("data.csv")

df.head()

df.info()

df.describe()

df.isna().sum()

df.drop_duplicates()

df["Date"] = pd.to_datetime(df["Date"])

df.groupby("Country")["Sales"].sum()

df.sort_values("Sales", ascending=False)

df.to_csv("output.csv", index=False)
```
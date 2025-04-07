# Internship-Day1
# 📊 Sales Data Cleaning & Preprocessing

## 🗂️ Dataset: `sales_data_sample.csv`

This project was carried out as part of my internship task to clean and preprocess a raw dataset using Python (Pandas). The dataset I worked on is called **"Sales Data Sample"**, which I downloaded from Kaggle.

### 📥 Dataset Source
The dataset was sourced from Kaggle's repository of publicly available datasets. Here's how I got it:

1. I visited [Kaggle - Sales Data Sample](https://www.kaggle.com/datasets/kyanyoga/sample-sales-data).
2. I downloaded the CSV file: `sales_data_sample.csv`.
3. I placed the dataset in my working directory to begin preprocessing.

---

## 🧹 Task Objectives

The goal was to clean and prepare the dataset, which included handling:

- Missing values  
- Duplicates  
- Inconsistent text formatting  
- Date formatting  
- Column renaming  
- Data type corrections  

---

## 🔧 Steps Performed

### 1. **Loaded the Dataset**
The dataset was loaded using `pandas.read_csv()`. Initially, I encountered a `UnicodeDecodeError`, which I fixed by adding the encoding parameter:
```python
import pandas as pd

df = pd.read_csv("sales_data_sample.csv", encoding='latin1')
```

## 🔍 2. Initial Data Overview

We used `df.info()` and `df.describe()` to explore the data:

```python
df.info()
df.describe()
```
✅ Total Rows: 2823

✅ Total Columns: 25

🚫 3. Missing Values
We inspected missing values using:


We used `df.isnull().sum()`

```python
# Dropping 'ADDRESSLINE2' due to 2521 missing values (not useful)
df.drop('ADDRESSLINE2', axis=1, inplace=True)

# 'STATE' had 1486 nulls - retained as is for potential future use

# 'POSTALCODE' had 76 nulls - filled with placeholder
df['POSTALCODE'].fillna('Unknown', inplace=True)

# 'TERRITORY' had 1074 nulls - filled with 'Not Assigned'
df['TERRITORY'].fillna('Not Assigned', inplace=True)
```


🔁 4. Duplicate Rows
Checked for duplicates using:

```python
df.duplicated().sum()
```
✅ Result: 0 duplicate rows found

✨ 5. Standardized Text Columns
To ensure uniformity, converted certain columns to lowercase and removed extra spaces:

```python
text_cols = ['STATUS', 'COUNTRY', 'TERRITORY', 'DEALSIZE']
for col in text_cols:
    df[col] = df[col].str.lower().str.strip()
```

🕒 6. Converted Date Format
The ORDERDATE column was in string format, so we converted it to datetime:

```python
df['ORDERDATE'] = pd.to_datetime(df['ORDERDATE'])
```


🏷️ 7. Renamed Columns
For better readability and coding convenience, all column headers were renamed:

```python
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")
```


🔢 8. Fixed Data Types
Converted necessary columns to proper data types:

```python
df['quantityordered'] = df['quantityordered'].astype(int)
df['msrp'] = df['msrp'].astype(int)
df['priceeach'] = df['priceeach'].astype(float)
df['sales'] = df['sales'].astype(float)

df['qtr_id'] = df['qtr_id'].astype(int)
df['month_id'] = df['month_id'].astype(int)
df['year_id'] = df['year_id'].astype(int)
```


✅ Summary of Changes
Task	                            Status
Missing Values Handled	               ✅
Duplicate Rows Removed	               ✅ (0 found)
Text Fields Standardized	           ✅
Date Format Converted	               ✅
Column Names Renamed	               ✅
Data Types Fixed	                   ✅



📌 Conclusions
The dataset is now clean, consistent, and ready for analysis or visualization.

All nulls are either handled logically or retained for future reference.

Column names are standardized and more readable.

The date field is in the correct datetime format.

No duplicates exist, ensuring data integrity.

This processed dataset is well-suited for building dashboards, running analytics, or applying machine learning models.


💻 Tools Used: 

Python

Pandas

Jupyter Notebook





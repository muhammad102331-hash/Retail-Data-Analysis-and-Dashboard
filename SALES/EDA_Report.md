# Exploratory Data Analysis (EDA) Report: Retail Sales Dataset

## 1. Data Overview

```python
import pandas as pd

# Load dataset
df = pd.read_csv('retail_sales_dataset.csv')
df.head()
```

---

## 2. Data Quality Check

```python
# Check for missing values
print(df.isnull().sum())

# Check data types
print(df.dtypes)

# Check for duplicate rows
print(df.duplicated().sum())
```

---

## 3. Basic Statistics

### 3.1 Transaction Statistics

```python
print(f"Total transactions: {df.shape[0]}")
print(f"Unique customers: {df['Customer ID'].nunique()}")
print(f"Date range: {df['Date'].min()} to {df['Date'].max()}")
```

### 3.2 Numeric Columns Summary

```python
numeric_cols = ['Age', 'Quantity', 'Price per Unit', 'Total Amount']
print(df[numeric_cols].describe())
```

### 3.3 Categorical Columns Summary

```python
print(df['Gender'].value_counts())
print(df['Product Category'].value_counts())
```

---

## 4. Univariate Analysis

### 4.1 Age Distribution

```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(6,4))
sns.histplot(df['Age'], bins=15, kde=True, color='skyblue')
plt.title('Customer Age Distribution')
plt.xlabel('Age')
plt.ylabel('Count')
plt.show()
```

### 4.2 Quantity and Price per Unit

```python
fig, axes = plt.subplots(1,2, figsize=(12,4))
sns.histplot(df['Quantity'], bins=10, ax=axes[0], color='lightgreen')
axes[0].set_title('Quantity Distribution')
sns.histplot(df['Price per Unit'], bins=15, ax=axes[1], color='orange')
axes[1].set_title('Price per Unit Distribution')
plt.tight_layout()
plt.show()
```

### 4.3 Gender Distribution

```python
sns.countplot(x='Gender', data=df, palette='pastel')
plt.title('Gender Distribution')
plt.show()
```

### 4.4 Product Category Distribution

```python
sns.countplot(x='Product Category', data=df, palette='muted')
plt.title('Product Category Distribution')
plt.show()
```

---

## 5. Bivariate Analysis

### 5.1 Sales by Product Category

```python
sales_by_category = df.groupby('Product Category')['Total Amount'].sum()
sales_by_category.plot(kind='bar', color=['purple','gold','turquoise'])
plt.title('Total Sales by Product Category')
plt.ylabel('Sales (Total Amount)')
plt.show()
```

### 5.2 Total Amount by Gender

```python
sns.boxplot(x='Gender', y='Total Amount', data=df, palette='coolwarm')
plt.title('Total Amount by Gender')
plt.show()
```

### 5.3 Age by Product Category

```python
sns.boxplot(x='Product Category', y='Age', data=df, palette='Set2')
plt.title('Customer Age by Product Category')
plt.show()
```

### 5.4 Quantity by Product Category

```python
sns.boxplot(x='Product Category', y='Quantity', data=df, palette='Blues')
plt.title('Quantity by Product Category')
plt.show()
```

---

## 6. Time Series Analysis

### 6.1 Sales Trend Over Time

```python
df['Date'] = pd.to_datetime(df['Date'])
monthly_sales = df.resample('M', on='Date')['Total Amount'].sum()
monthly_sales.plot(marker='o', figsize=(12,5), color='coral')
plt.title('Monthly Sales Trend')
plt.ylabel('Total Sales')
plt.xlabel('Month')
plt.show()
```

---

## 7. Outlier Detection

```python
# Outliers in "Total Amount"
sns.boxplot(x='Total Amount', data=df, color='red')
plt.title('Outlier Detection: Total Amount')
plt.show()
```

---

## 8. Interesting Observations (Fill after running code)

- Most customers are (gender), and mainly purchase (product category).
- The majority of transactions are for customers aged (age range).
- Highest revenue comes from (category).
- There are outliers in "Total Amount" due to bulk purchases.
- Some months/weeks have spikes in sales, suggesting potential seasonality.

---

## 9. Recommendations for Business

- Focus marketing efforts on age groups and categories with highest sales.
- Investigate outliers for bulk purchase opportunities.
- Identify slow-selling product categories for possible improvement.

---

## 10. Next Steps

- Segment customers for targeted marketing.
- Analyze repeat purchases and customer lifetime value.
- Compare seasonal sales (e.g., pre/post holidays).

---

## Appendix: Save Cleaned Data

```python
# Remove duplicates for further analysis
df_clean = df.drop_duplicates()
df_clean.to_csv('retail_sales_clean.csv', index=False)
```

---

**End of EDA Report**
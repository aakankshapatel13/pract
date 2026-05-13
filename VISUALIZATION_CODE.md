# Python Visualization Code Snippets (Matplotlib & Pandas)

Here is the code for the 5 most common plots used in Data Analysis.

---

## 1. Bar Chart (For Comparison)
Best for: Comparing categories (e.g., Sales by Region).
```python
# Assuming 'df' is your DataFrame
df['Pclass'].value_counts().plot(kind='bar', color='skyblue')
plt.title("Count of Passengers per Class")
plt.xlabel("Class")
plt.ylabel("Count")
plt.show()
```

---

## 2. Pie Chart (For Proportions)
Best for: Showing parts of a whole (e.g., Gender distribution).
```python
df['Sex'].value_counts().plot(kind='pie', autopct='%1.1f%%')
plt.title("Gender Distribution on Titanic")
plt.ylabel("") # Hides the column name on the side
plt.show()
```

---

## 3. Histogram (For Distribution)
Best for: Seeing the spread of numerical data (e.g., Age groups).
```python
df['Age'].plot(kind='hist', bins=10, color='orange', edgecolor='black')
plt.title("Age Distribution of Passengers")
plt.xlabel("Age")
plt.show()
```

---

## 4. Scatter Plot (For Correlation)
Best for: Seeing the relationship between two numbers (e.g., Age vs. Fare).
```python
# Note: Requires two numerical columns
plt.scatter(df['Age'], df['Id'], alpha=0.5) 
plt.title("Relationship between Age and Passenger ID")
plt.xlabel("Age")
plt.ylabel("ID")
plt.show()
```

---

## 5. Line Chart (For Trends)
Best for: Showing changes over time (Time Series).
```python
# Sorting by ID to simulate a sequence/trend
df.sort_values('Id')['Age'].plot(kind='line', marker='o')
plt.title("Age Trend across Passenger IDs")
plt.xlabel("Passenger Index")
plt.ylabel("Age")
plt.show()
```

---

## 6. Box Plot (For Outliers)
Best for: Seeing the range, median, and outliers in your data.
```python
df.boxplot(column='Age', by='Pclass')
plt.title("Age Distribution by Class")
plt.suptitle("") # Cleans up the title
plt.show()
```

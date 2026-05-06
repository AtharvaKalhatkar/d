# Practical 4 — Data Visualization (Matplotlib & Seaborn)

## Cell 1 — Import Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

## Cell 2 — Load Dataset
```python
df = pd.read_csv(r'C:\Users\DELL\Downloads\heart.csv')
print(df.shape)
df.head()
```

## Cell 3 — Histogram
```python
plt.figure(figsize=(8,5))
plt.hist(df['age'], bins=20, color='skyblue', edgecolor='black')
plt.title('Age Distribution')
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.show()
```

## Cell 4 — Bar Chart
```python
plt.figure(figsize=(8,5))
df['target'].value_counts().plot(kind='bar', color=['green','red'])
plt.title('Heart Disease Count')
plt.xlabel('Target (0=No, 1=Yes)')
plt.ylabel('Count')
plt.show()
```

## Cell 5 — Scatter Plot
```python
plt.figure(figsize=(8,5))
plt.scatter(df['age'], df['chol'], color='purple', alpha=0.5)
plt.title('Age vs Cholesterol')
plt.xlabel('Age')
plt.ylabel('Cholesterol')
plt.show()
```

## Cell 6 — Boxplot
```python
plt.figure(figsize=(8,5))
sns.boxplot(x='target', y='age', data=df, palette='Set2')
plt.title('Age vs Heart Disease')
plt.xlabel('Target (0=No, 1=Yes)')
plt.ylabel('Age')
plt.show()
```

## Cell 7 — Heatmap
```python
plt.figure(figsize=(10,8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm', fmt='.2f')
plt.title('Correlation Heatmap')
plt.show()
```

## Cell 8 — Pairplot
```python
sns.pairplot(df[['age','chol','trestbps','target']], hue='target')
plt.suptitle('Pairplot of Heart Disease Features', y=1.02)
plt.show()
```

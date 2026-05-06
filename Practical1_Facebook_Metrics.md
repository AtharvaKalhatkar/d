# Practical 1 — Facebook Metrics Dataset

## Cell 1 — Import Libraries
```python
import pandas as pd
import numpy as np
```

## Cell 2 — Load Dataset
```python
df = pd.read_csv(r'C:\Users\DELL\Downloads\dataset_Facebook.csv', sep=';')
print(df.shape)
df.head()
```

## Cell 3 — a) Create Data Subsets
```python
photo_posts = df[df['Type'] == 'Photo']
print("Photo posts shape:", photo_posts.shape)
popular_posts = df[df['like'] > 100]
print("Popular posts shape:", popular_posts.shape)
photo_posts.head()
```

## Cell 4 — b) Merge Data
```python
df1 = df[['Type', 'Category', 'Post Month', 'Post Weekday', 'Post Hour', 'Paid']].copy()
df2 = df[['like', 'share', 'comment', 'Total Interactions']].copy()
df1['id'] = range(len(df1))
df2['id'] = range(len(df2))
merged_df = pd.merge(df1, df2, on='id')
print("Merged shape:", merged_df.shape)
merged_df.head()
```

## Cell 5 — c) Sort Data
```python
sorted_df = df.sort_values(by='like', ascending=False)
print("Top 5 most liked posts:")
sorted_df[['Type', 'like', 'share', 'comment']].head()
```

## Cell 6 — d) Transpose Data
```python
transposed = df[['Type', 'like', 'share', 'comment']].head().T
print("Transposed shape:", transposed.shape)
transposed
```

## Cell 7 — e) Shape and Reshape
```python
print("Original DataFrame shape:", df.shape)
data_array = df[['like', 'share', 'comment']].dropna().values
print("Array shape:", data_array.shape)
reshaped = data_array.reshape(-1, 1)
print("Reshaped shape:", reshaped.shape)
```

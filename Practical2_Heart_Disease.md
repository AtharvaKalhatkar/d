# Practical 2 — Heart Disease Dataset

## Cell 1 — Import Libraries
```python
import pandas as pd
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
```

## Cell 2 — Load Dataset
```python
df = pd.read_csv(r'C:\Users\DELL\Downloads\heart.csv')
print(df.shape)
df.head()
```

## Cell 3 — a) Data Cleaning
```python
df.fillna(df.mean(numeric_only=True), inplace=True)
df.drop_duplicates(inplace=True)
print(df.isnull().sum())
```

## Cell 4 — b) Data Integration
```python
df1 = df.iloc[:100]
df2 = df.iloc[100:]
df = pd.concat([df1, df2], ignore_index=True)
print(df.shape)
```

## Cell 5 — c) Data Transformation
```python
scaler = StandardScaler()
df[['age','chol','trestbps']] = scaler.fit_transform(df[['age','chol','trestbps']])
df.head()
```

## Cell 6 — d) Error Correcting
```python
print(df.isnull().sum())
print(df.duplicated().sum())
print(df.dtypes)
```

## Cell 7 — e) Model Building
```python
X = df.drop('target', axis=1)
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)
print("Accuracy:", accuracy_score(y_test, model.predict(X_test)))
```

---
title: 'Multiple Linear Regression (Boston Housing Dataset)'
categories: [Data Science, Statistical Analysis]
tags: [regression, multiple regression, python]
math: 'True'
img_path: "/assets/img/posting"
---

<div align=left>
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Jupyter%20Notebook-F37626?logo=jupyter&logoColor=white">
  <img src="https://img.shields.io/badge/Windows-000000?logo=windows&logoColor=white">
</div>

---

## Configuration
### Data Preprocessing

```python
from sklearn import datasets
from sklearn import linear_model
from sklearn.metrics import mean_squared_error
import pandas as pd

boston = datasets.load_boston()
X = pd.DataFrame(boston.data)
X.columns = boston.feature_names
y = pd.DataFrame(boston.target)
y.columns = ['PRICE']
y = y['PRICE']
```

Use Boston Housing Data from scikit-learm to predict house prices.

<br>

## Analysis
```python
linear_regression = linear_model.LinearRegression()
linear_regression.fit(X=pd.DataFrame(X), y=y)
prediction = linear_regression.predict(X=pd.DataFrame(X))

a = linear_regression.intercept_
b = linear_regression.coef_

print("a : %.2f" %a)
print("b : %.2f" %b)
```
$y=a+b_1x_1+b_2x_2+...+b_{13}x_{13}$

![result](2019-05-04_boston-1.png){: weight="50%" height="50%"}

<br>
## Performation Evaluation
### Residual Calculation
```python
residuals = y - prediction
residuals.describe()
```

![residuals](2019-05-04_boston-2.png){: weight="20%" height="20%"}

### Coefficient of Determination Calculation
```python
SSE = (residuals**2).sum()
SST = ((y-y.mean())**2).sum()
r2 = 1 - SSE/SST

print("R Squared : %.3f" %r2)
```
R Squred : 0.741

### MSE Calculation
```python
score = linear_regression.score(X=pd.DataFrame(X), y=y)
MSE = mean_squared_error(prediction, y)

print("Score : %.3f" %score)
print("MSE : %.2f" %MSE)
```
Score : 0.741
MSE : 21.89

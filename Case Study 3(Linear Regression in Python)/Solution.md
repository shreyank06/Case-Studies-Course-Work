```python
import numpy as np
import matplotlib.pyplot as plt  # To visualize
import pandas as pd  # To read data
from sklearn.linear_model import LinearRegression
from sklearn import linear_model
import statsmodels.api as sm

import sys
assert sys.version_info >= (3,6), 'You need to be running at least Python version 3.6'

```


```python
with open('Data.txt', 'r') as d:
    
    data = []
    
    for line in d:
        
        line = line[:-1]
        line = (line.split(','))
        
        data.append(line)
        
one = ['Week', 'Sales', 'TV', 'Radio', 'Fuel Volume', 'Fuel Price', 'Temp', 'Prec', 'Holiday', 'Visits(1 or 2)']

dataFrame = pd.DataFrame(data, columns = one)

print(dataFrame)
```

      Week  Sales     TV  Radio Fuel Volume Fuel Price  Temp  Prec Holiday  \
    0   26  24864   74.5   66.5       61825     104.24  27.9   0.9       1   
    1   27  23809   74.5   66.5       62617     103.97  27.7   1.3       1   
    2   28  24476   90.0   75.0       60227     107.48  29.1   4.8       1   
    3   29  25279   90.0   75.0       63273     111.75  30.0   3.1       1   
    4   30  26263   90.0   75.0       65196     109.08  29.3   0.0       1   
    5   18  23688  160.0  208.0       65052     130.95  16.8  12.7       1   
    6   19  23922  150.0  208.0       63214     129.06  17.3  14.6       1   
    7   20  24421    0.0    0.0       63379     129.28  19.7   5.9       0   
    8   21  26197    0.0    0.0       63623     127.19  21.1   6.1       0   
    9   22  26765  180.0  237.0       62661     129.19  21.8   7.3       0   
    
      Visits(1 or 2)  
    0            7.0  
    1            7.0  
    2            5.9  
    3            5.9  
    4            5.9  
    5            6.0  
    6            6.0  
    7            6.0  
    8            6.0  
    9             4.  
    


```python
with open('Data.txt', 'r') as d:
    
    data = []
    
    for line in d:
        
        line = line[:-1]
        line = (line.split(','))
        
        data.append(line)
        
one = ['Week', 'Sales', 'TV', 'Radio', 'Fuel Volume', 'Fuel Price', 'Temp', 'Prec', 'Holiday', 'Visits(1 or 2)']

dataFrame = pd.DataFrame(data, columns = one)

#dataFrame.sort_values(by = ['Week'], ascending = True)

X = dataFrame[["Radio", "Temp"]]
Y = dataFrame["Sales"]

X = np.array(X)
Y = np.array(Y)

X = X.astype(np.double)
Y = Y.astype(np.double)

X = sm.add_constant(X)

est=sm.OLS(Y, X)

est = est.fit()
est.summary()
```

    C:\Users\Mayank\anaconda3\lib\site-packages\scipy\stats\stats.py:1604: UserWarning: kurtosistest only valid for n>=20 ... continuing anyway, n=10
      "anyway, n=%i" % int(n))
    




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>            <td>y</td>        <th>  R-squared:         </th> <td>   0.059</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>  -0.210</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>  0.2193</td>
</tr>
<tr>
  <th>Date:</th>             <td>Fri, 30 Apr 2021</td> <th>  Prob (F-statistic):</th>  <td> 0.808</td> 
</tr>
<tr>
  <th>Time:</th>                 <td>09:35:32</td>     <th>  Log-Likelihood:    </th> <td> -83.503</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    10</td>      <th>  AIC:               </th> <td>   173.0</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>     7</td>      <th>  BIC:               </th> <td>   173.9</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     2</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
    <td></td>       <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th> <td> 2.359e+04</td> <td> 2387.808</td> <td>    9.880</td> <td> 0.000</td> <td> 1.79e+04</td> <td> 2.92e+04</td>
</tr>
<tr>
  <th>x1</th>    <td>    0.5598</td> <td>    5.274</td> <td>    0.106</td> <td> 0.918</td> <td>  -11.910</td> <td>   13.030</td>
</tr>
<tr>
  <th>x2</th>    <td>   54.8190</td> <td>   86.264</td> <td>    0.635</td> <td> 0.545</td> <td> -149.163</td> <td>  258.802</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 1.410</td> <th>  Durbin-Watson:     </th> <td>   0.975</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.494</td> <th>  Jarque-Bera (JB):  </th> <td>   1.009</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 0.585</td> <th>  Prob(JB):          </th> <td>   0.604</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 1.974</td> <th>  Cond. No.          </th> <td>    809.</td>
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.




```python
with open('Data.txt', 'r') as d:
    
    data = []
    
    for line in d:
        
        line = line[:-1]
        line = (line.split(','))
        
        data.append(line)
        
one = ['Week', 'Sales', 'TV', 'Radio', 'Fuel Volume', 'Fuel Price', 'Temp', 'Prec', 'Holiday', 'Visits(1 or 2)']

dataFrame = pd.DataFrame(data, columns = one)

#dataFrame.sort_values(by = ['Week'], ascending = True)

X = dataFrame[["TV", "Temp"]]
Y = dataFrame["Sales"]

X = np.array(X)
Y = np.array(Y)

X = X.astype(np.double)
Y = Y.astype(np.double)

X = sm.add_constant(X)

est=sm.OLS(Y, X)

est = est.fit()
est.summary()

```

    C:\Users\Mayank\anaconda3\lib\site-packages\scipy\stats\stats.py:1604: UserWarning: kurtosistest only valid for n>=20 ... continuing anyway, n=10
      "anyway, n=%i" % int(n))
    




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>            <td>y</td>        <th>  R-squared:         </th> <td>   0.057</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>  -0.212</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>  0.2135</td>
</tr>
<tr>
  <th>Date:</th>             <td>Fri, 30 Apr 2021</td> <th>  Prob (F-statistic):</th>  <td> 0.813</td> 
</tr>
<tr>
  <th>Time:</th>                 <td>09:35:33</td>     <th>  Log-Likelihood:    </th> <td> -83.511</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>    10</td>      <th>  AIC:               </th> <td>   173.0</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>     7</td>      <th>  BIC:               </th> <td>   173.9</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     2</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
    <td></td>       <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th> <td> 2.376e+04</td> <td> 2162.096</td> <td>   10.989</td> <td> 0.000</td> <td> 1.86e+04</td> <td> 2.89e+04</td>
</tr>
<tr>
  <th>x1</th>    <td>   -0.1008</td> <td>    6.853</td> <td>   -0.015</td> <td> 0.989</td> <td>  -16.306</td> <td>   16.105</td>
</tr>
<tr>
  <th>x2</th>    <td>   50.6304</td> <td>   79.474</td> <td>    0.637</td> <td> 0.544</td> <td> -137.297</td> <td>  238.558</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 1.399</td> <th>  Durbin-Watson:     </th> <td>   0.971</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.497</td> <th>  Jarque-Bera (JB):  </th> <td>   1.021</td>
</tr>
<tr>
  <th>Skew:</th>          <td> 0.627</td> <th>  Prob(JB):          </th> <td>   0.600</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 2.064</td> <th>  Cond. No.          </th> <td>    612.</td>
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.




```python
linear_regressor = LinearRegression()  # create object for the class
linear_regressor.fit(X, Y)  # perform linear regression
Y_pred = linear_regressor.predict(X)  # make predictions


plt.scatter(X, Y)
plt.plot(X, Y_pred, color='red')
plt.show()


df1 = dataFrame[['Sales', 'Fuel Volume']]

lr = LinearRegression()

lr.fit(df1["Fuel Volume"], df1["Sales"])

plt.scatter(df1["Fuel Volume"], df1["Sales"])
#plt.plot(df1["Sales"], Y_pred, color = 'red')
plt.show
```


```python

```

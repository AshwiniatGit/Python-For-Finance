## Calculating Portfolio Risk

Calculate the risk of an equally weighted portfolio composed of Microsoft and Apple. The data can be obtained from Yahoo Finance for the period 1st of January 2007 until today. 

*Hint: The code we went through in the lecture is what you need here. You will need to import the data first. The previous lessons could be a good reference point for that! :) *


```python
import numpy as np
import pandas as pd
from pandas_datareader import data as wb
import matplotlib.pyplot as plt
tickers = ['MSFT','AAPL']
data = pd.DataFrame()
for t in tickers:
    data[t] = wb.DataReader(t, data_source='yahoo', start='2007-1-1')['Adj Close']
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MSFT</th>
      <th>AAPL</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2007-01-03</th>
      <td>22.185307</td>
      <td>10.363638</td>
    </tr>
    <tr>
      <th>2007-01-04</th>
      <td>22.148153</td>
      <td>10.593664</td>
    </tr>
    <tr>
      <th>2007-01-05</th>
      <td>22.021847</td>
      <td>10.518225</td>
    </tr>
    <tr>
      <th>2007-01-08</th>
      <td>22.237307</td>
      <td>10.570165</td>
    </tr>
    <tr>
      <th>2007-01-09</th>
      <td>22.259609</td>
      <td>11.448232</td>
    </tr>
  </tbody>
</table>
</div>



## MSFT


```python
returns = pd.DataFrame()
returns['MSFT'] = (data['MSFT']/data['MSFT'].shift(1))-1
returns['MSFT']
```




    Date
    2007-01-03         NaN
    2007-01-04   -0.001675
    2007-01-05   -0.005703
    2007-01-08    0.009784
    2007-01-09    0.001003
                    ...   
    2020-05-06    0.009847
    2020-05-07    0.005807
    2020-05-08    0.005882
    2020-05-11    0.011154
    2020-05-12   -0.022652
    Name: MSFT, Length: 3363, dtype: float64



## Apple


```python
returns['AAPL'] = (data['AAPL']/data['AAPL'].shift(1))-1
returns['AAPL']
```




    Date
    2007-01-03         NaN
    2007-01-04    0.022196
    2007-01-05   -0.007121
    2007-01-08    0.004938
    2007-01-09    0.083070
                    ...   
    2020-05-06    0.010317
    2020-05-07    0.010345
    2020-05-08    0.023802
    2020-05-11    0.015735
    2020-05-12   -0.011428
    Name: AAPL, Length: 3363, dtype: float64



***

## Covariance and Correlation


\begin{eqnarray*}
Covariance Matrix: \  \   
\Sigma = \begin{bmatrix}
        \sigma_{1}^2 \ \sigma_{12} \ \dots \ \sigma_{1I} \\
        \sigma_{21} \ \sigma_{2}^2 \ \dots \ \sigma_{2I} \\
        \vdots \ \vdots \ \ddots \ \vdots \\
        \sigma_{I1} \ \sigma_{I2} \ \dots \ \sigma_{I}^2
    \end{bmatrix}
\end{eqnarray*}

*****

Covariance matrix:

***

Correlation matrix:


```python
cov_matrix = returns.cov()
cov_matrix
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MSFT</th>
      <th>AAPL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MSFT</th>
      <td>0.000321</td>
      <td>0.000195</td>
    </tr>
    <tr>
      <th>AAPL</th>
      <td>0.000195</td>
      <td>0.000414</td>
    </tr>
  </tbody>
</table>
</div>



## Calculating Portfolio Risk

Equal weigthing scheme:


```python
weights = np.array([0.5,0.5])
```

Portfolio Variance:


```python
portfolio_var = np.dot(weights.T, np.dot(returns.cov() * 250, weights))
portfolio_var
```




    0.07036771881822003



Portfolio Volatility:


```python
portfolio_vol = np.dot(weights.T, np.dot(returns.cov() * 250, weights)) ** 0.5
portfolio_vol
```




    0.2652691441125787




```python
print('The Risk for this portfolio is:',str(round(portfolio_vol*100,2)),'%')
```

    The Risk for this portfolio is: 26.53 %
    

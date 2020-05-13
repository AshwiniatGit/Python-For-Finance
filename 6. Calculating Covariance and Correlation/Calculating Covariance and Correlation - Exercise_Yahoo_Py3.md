## Calculating Covariance and Correlation

Consider a portfolio composed of *Walmart* and *Facebook*. Do you expect the returns of these companies to show high or low covariance? Or, could you guess what the correlation would be? Will it be closer to 0 or closer to 1? 

Begin by extracting data for Walmart and Facebook from the 1st of January 2014 until today.


```python
import numpy as np
import pandas as pd
from pandas_datareader import data as wb
import matplotlib.pyplot as plt
```

    C:\Users\aks13\anaconda3\lib\site-packages\pandas_datareader\compat\__init__.py:7: FutureWarning: pandas.util.testing is deprecated. Use the functions in the public API at pandas.testing instead.
      from pandas.util.testing import assert_frame_equal
    

Repeat the process we went through in the lecture for these two stocks. How would you explain the difference between their means and their standard deviations?


```python
tickers = ['WMT','FB']
data = pd.DataFrame()
for t in tickers:
    data[t] = wb.DataReader(t, data_source='yahoo', start='2005-1-1')['Adj Close']
```


```python
returns = pd.DataFrame()
for t in tickers:
    returns[t] = (data[t]/data[t].shift(1))-1
returns
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
      <th>WMT</th>
      <th>FB</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2004-12-31</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2005-01-03</th>
      <td>0.010034</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2005-01-04</th>
      <td>-0.002437</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2005-01-05</th>
      <td>0.001316</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2005-01-06</th>
      <td>0.014261</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2020-05-06</th>
      <td>-0.011465</td>
      <td>0.006761</td>
    </tr>
    <tr>
      <th>2020-05-07</th>
      <td>-0.007087</td>
      <td>0.013383</td>
    </tr>
    <tr>
      <th>2020-05-08</th>
      <td>0.008614</td>
      <td>0.005160</td>
    </tr>
    <tr>
      <th>2020-05-11</th>
      <td>0.005938</td>
      <td>0.003909</td>
    </tr>
    <tr>
      <th>2020-05-12</th>
      <td>0.000889</td>
      <td>-0.014448</td>
    </tr>
  </tbody>
</table>
<p>3867 rows × 2 columns</p>
</div>



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

Covariance matrix:


```python
cov_matrix = returns.cov()
print(cov_matrix)
cov_matrix_annual = returns.cov() * 250
print(cov_matrix_annual)
```

              WMT        FB
    WMT  0.000161  0.000047
    FB   0.000047  0.000552
              WMT        FB
    WMT  0.040183  0.011727
    FB   0.011727  0.138103
    

Correlation matrix:


```python
corr_matrix = returns.corr()
corr_matrix
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
      <th>WMT</th>
      <th>FB</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>WMT</th>
      <td>1.000000</td>
      <td>0.160737</td>
    </tr>
    <tr>
      <th>FB</th>
      <td>0.160737</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



Would you consider investing in such a portfolio?

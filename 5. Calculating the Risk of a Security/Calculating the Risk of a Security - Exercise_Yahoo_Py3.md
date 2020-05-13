## Calculating the Risk of a Security

*Suggested Answers follow (usually there are multiple ways to solve a problem in Python).*

Download the data for Search Results Finance results Procter & Gamble Co (‘PG’) from Yahoo Finance for the period ‘2000-1-1’ until today. <br />
Assess the daily and the annual risk of ‘PG’. Repeat the exercise for Search Results Finance results Beiersdorf AG for the same timeframe. 


```python
import numpy as np
import pandas as pd
from pandas_datareader import data as wb
import matplotlib.pyplot as plt
tickers = ['PG','BEI.DE']
data  = pd.DataFrame()
for t in tickers:
    data[t] = wb.DataReader(t, data_source='yahoo', start='2007-1-1')['Adj Close']
returns = np.log(data / data.shift(1))
returns.head()
```

    C:\Users\aks13\anaconda3\lib\site-packages\pandas_datareader\compat\__init__.py:7: FutureWarning: pandas.util.testing is deprecated. Use the functions in the public API at pandas.testing instead.
      from pandas.util.testing import assert_frame_equal
    




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
      <th>PG</th>
      <th>BEI.DE</th>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2007-01-04</th>
      <td>-0.007621</td>
      <td>0.006544</td>
    </tr>
    <tr>
      <th>2007-01-05</th>
      <td>-0.008624</td>
      <td>-0.020772</td>
    </tr>
    <tr>
      <th>2007-01-08</th>
      <td>0.002202</td>
      <td>0.000202</td>
    </tr>
    <tr>
      <th>2007-01-09</th>
      <td>-0.002517</td>
      <td>-0.022858</td>
    </tr>
  </tbody>
</table>
</div>



### PG

Daily risk:


```python
returns['PG'].std() ** 0.5
```




    0.10934922995596112



Annual risk:


```python
returns['PG'].std()*250 ** 0.5
```




    0.1890607874598366



### BEI.DE

Daily risk:


```python
returns['BEI.DE'].std()** 0.5
```




    0.11735323464132329



Annual risk:


```python
returns['BEI.DE'].std()*250 ** 0.5
```




    0.21775098774925705



******

Store the volatilities of the two stocks in an array called “vols”.


```python
vols = np.array(returns[['PG','BEI.DE']].std()*250 ** 0.5)
vols
```




    array([0.18906079, 0.21775099])



How are the two risk values different?

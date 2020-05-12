```python
import numpy as np
import pandas as pd
from pandas_datareader import data as wb
import matplotlib.pyplot as plt
```

    C:\Users\aks13\anaconda3\lib\site-packages\pandas_datareader\compat\__init__.py:7: FutureWarning: pandas.util.testing is deprecated. Use the functions in the public API at pandas.testing instead.
      from pandas.util.testing import assert_frame_equal
    


```python
tickers = ['PG','BEI.DE']
data  = pd.DataFrame()
for t in tickers:
    data[t] = wb.DataReader(t, data_source='yahoo', start='2007-1-1')['Adj Close']
```


```python
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
      <td>43.143341</td>
      <td>39.576427</td>
    </tr>
    <tr>
      <th>2007-01-04</th>
      <td>42.815781</td>
      <td>39.836281</td>
    </tr>
    <tr>
      <th>2007-01-05</th>
      <td>42.448109</td>
      <td>39.017349</td>
    </tr>
    <tr>
      <th>2007-01-08</th>
      <td>42.541702</td>
      <td>39.025219</td>
    </tr>
    <tr>
      <th>2007-01-09</th>
      <td>42.434750</td>
      <td>38.143303</td>
    </tr>
  </tbody>
</table>
</div>




```python
returns = np.log(data / data.shift(1))
returns.head()
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




```python
returns['PG'].mean()
```




    0.0002925010555275492




```python
returns['PG'].mean()*250
```




    0.07312526388188731




```python
returns['PG'].std()
```




    0.011958429998009236




```python
returns['PG'].std()*250 ** 0.5
```




    0.18907938016696002




```python
returns['BEI.DE'].mean()
```




    0.0002479240365699525




```python
returns['BEI.DE'].mean()*250
```




    0.06198100914248812




```python
returns['BEI.DE'].std()
```




    0.013773597716189889




```python
returns['BEI.DE'].std()*250 ** 0.5
```




    0.21777970179026748




```python
returns[['PG','BEI.DE']].mean()*250
```




    PG        0.073125
    BEI.DE    0.061981
    dtype: float64




```python
returns[['PG','BEI.DE']].std()*250 ** 0.5
```




    PG        0.189079
    BEI.DE    0.217780
    dtype: float64



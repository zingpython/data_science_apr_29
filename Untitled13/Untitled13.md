

```python
import pandas as pd
import numpy as np
import datetime
from datetime import date
import matplotlib.pyplot as plt
import pandas_datareader.data as web
```


```python
start = date(2014, 1, 1)
end = date.today()
```


```python
portfolio = ["AAPL","MSFT","GE","BAC", "VZ"]
data = pd.DataFrame()
for co in portfolio:
    data[co] = web.DataReader(co, 'yahoo', start, end)["Adj Close"]
```


```python
(data/data.ix[0] * 100).plot()
plt.show()
```


![png](output_3_0.png)



```python
#Calculating returns
returns = np.log(data/data.shift(1))
returns.tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>MSFT</th>
      <th>GE</th>
      <th>BAC</th>
      <th>VZ</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-05-01</th>
      <td>0.020192</td>
      <td>0.013781</td>
      <td>-0.001726</td>
      <td>0.011502</td>
      <td>-0.000654</td>
    </tr>
    <tr>
      <th>2017-05-02</th>
      <td>0.006325</td>
      <td>-0.001586</td>
      <td>0.001726</td>
      <td>-0.003394</td>
      <td>0.000654</td>
    </tr>
    <tr>
      <th>2017-05-03</th>
      <td>-0.003055</td>
      <td>-0.003180</td>
      <td>0.008245</td>
      <td>0.010148</td>
      <td>0.005214</td>
    </tr>
    <tr>
      <th>2017-05-04</th>
      <td>-0.003610</td>
      <td>-0.003916</td>
      <td>-0.001027</td>
      <td>0.003360</td>
      <td>-0.005868</td>
    </tr>
    <tr>
      <th>2017-05-05</th>
      <td>0.016448</td>
      <td>0.002757</td>
      <td>0.000685</td>
      <td>-0.004623</td>
      <td>0.017501</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Mean-variance of returns
#Since we have significant differences in performance, 
#we have to use 252 trading days to annualize the daily returns 
returns.mean() * 252
```




    AAPL    0.209165
    MSFT    0.211507
    GE      0.050364
    BAC     0.127737
    VZ      0.032854
    dtype: float64




```python
#Building covariance matrix
returns.cov() * 252
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>MSFT</th>
      <th>GE</th>
      <th>BAC</th>
      <th>VZ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AAPL</th>
      <td>0.053934</td>
      <td>0.022737</td>
      <td>0.014945</td>
      <td>0.020078</td>
      <td>0.009543</td>
    </tr>
    <tr>
      <th>MSFT</th>
      <td>0.022737</td>
      <td>0.050820</td>
      <td>0.017846</td>
      <td>0.023855</td>
      <td>0.013504</td>
    </tr>
    <tr>
      <th>GE</th>
      <td>0.014945</td>
      <td>0.017846</td>
      <td>0.031406</td>
      <td>0.023534</td>
      <td>0.010889</td>
    </tr>
    <tr>
      <th>BAC</th>
      <td>0.020078</td>
      <td>0.023855</td>
      <td>0.023534</td>
      <td>0.070215</td>
      <td>0.009420</td>
    </tr>
    <tr>
      <th>VZ</th>
      <td>0.009543</td>
      <td>0.013504</td>
      <td>0.010889</td>
      <td>0.009420</td>
      <td>0.023941</td>
    </tr>
  </tbody>
</table>
</div>




```python
#We assume that we do not open short position and we divide our money equally divided among 5 stocks
#So we generate 5 random numbers and then normalize them so that values would sum up 100% net oper assets
noa = len(portfolio)
weights = np.random.random(noa)
weights /= np.sum(weights)
weights
```




    array([ 0.104435  ,  0.16569197,  0.3122453 ,  0.17212976,  0.24549797])




```python
#Calculating Expected portfolio return based on the weights
expected_return = np.sum(returns.mean() * weights) * 252
expected_return
```




    0.10266828670189905




```python
#Now lets calculate Expected portfolio variance using our covariance matrix
#we use np.dot -  gets us a product of two matrices
expected_variance = np.dot(weights.T, np.dot(returns.cov() * 252, weights))
expected_variance
```




    0.020842618382137405




```python
#Now we calculate expected standard deviation or volatility 
volatility = np.sqrt(np.dot(weights.T, np.dot(returns.cov() * 252, weights))) 
volatility
```




    0.14436972806699264




```python
#Monte Carlo simulation to generate random portfolio weight vectors on larger scale
#For every simulated allocation we record the resulting portfolio return and variance
#We assume Risk free is 0
mrets = []
mvols = []
for i in range(2500):
    weights = np.random.random(noa)
    weights /= np.sum(weights)
    mrets.append(np.sum(returns.mean() * weights) * 252)
    mvols.append(np.sqrt(np.dot(weights.T, np.dot(returns.cov() * 252, weights ))))
    
mrets = np.array(mrets)
mvols = np.array(mvols)
```


```python
#Lets plot it
plt.figure()
plt.scatter(mvols, mrets, c=mrets / mvols, marker='o')
plt.grid(True)
plt.xlabel('Expected volatility')
plt.ylabel('Expected return')
plt.colorbar(label="Sharpe ratio")
plt.show()
```


![png](output_12_0.png)



```python

```



```python
#import pandas
import pandas as pd 
```


```python
# create Data Frame object
stocks = ["IBM", "APPLE", "TWTTR", "GE", "MSFT"]
prices = [115.00, 119.14, 19.77, 25.99, 26]
```


```python
portfolio = list(zip(stocks,prices))
print(portfolio)
```

    [('IBM', 115.0), ('APPLE', 119.14), ('TWTTR', 19.77), ('GE', 25.99), ('MSFT', 26)]



```python
df = pd.DataFrame(data=portfolio, columns=['Stocks', 'Prices'])
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stocks</th>
      <th>Prices</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>IBM</td>
      <td>115.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>APPLE</td>
      <td>119.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>TWTTR</td>
      <td>19.77</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GE</td>
      <td>25.99</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MSFT</td>
      <td>26.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
# lets add another column
df["Volume"] = [40,36,23,44,25]
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stocks</th>
      <th>Prices</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>IBM</td>
      <td>115.00</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1</th>
      <td>APPLE</td>
      <td>119.14</td>
      <td>36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>TWTTR</td>
      <td>19.77</td>
      <td>23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GE</td>
      <td>25.99</td>
      <td>44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MSFT</td>
      <td>26.00</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# we can change index
df.index = ['a','b','c','d','e']
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stocks</th>
      <th>Prices</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>IBM</td>
      <td>115.00</td>
      <td>40</td>
    </tr>
    <tr>
      <th>b</th>
      <td>APPLE</td>
      <td>119.14</td>
      <td>36</td>
    </tr>
    <tr>
      <th>c</th>
      <td>TWTTR</td>
      <td>19.77</td>
      <td>23</td>
    </tr>
    <tr>
      <th>d</th>
      <td>GE</td>
      <td>25.99</td>
      <td>44</td>
    </tr>
    <tr>
      <th>e</th>
      <td>MSFT</td>
      <td>26.00</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python
# slicing DataFrame objects
df.Stocks
```




    a      IBM
    b    APPLE
    c    TWTTR
    d       GE
    e     MSFT
    Name: Stocks, dtype: object




```python
# slicing with square brackets
df["Stocks"]
```




    a      IBM
    b    APPLE
    c    TWTTR
    d       GE
    e     MSFT
    Name: Stocks, dtype: object




```python
# indexing using square brackets
# column label and index
df["Stocks"]['c']
```




    'TWTTR'




```python
# column can be an attribute
df.Stocks['c']
```




    'TWTTR'




```python
# more officiant way is to use .loc - indexing by labels
df.loc['c']
```




    Stocks    TWTTR
    Prices    19.77
    Volume       23
    Name: c, dtype: object




```python
df.loc['c', 'Prices']
```




    19.77




```python
# or .iloc - indexing by index positions, row and column
print(df)
df.iloc[4,1]
```

      Stocks  Prices  Volume
    a    IBM  115.00      40
    b  APPLE  119.14      36
    c  TWTTR   19.77      23
    d     GE   25.99      44
    e   MSFT   26.00      25





    26.0




```python
df.iloc[-1,1]
```




    26.0




```python
# you can create new DataFrame or Series
df_new = df[['Stocks','Volume']]
df_new
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Stocks</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>IBM</td>
      <td>40</td>
    </tr>
    <tr>
      <th>b</th>
      <td>APPLE</td>
      <td>36</td>
    </tr>
    <tr>
      <th>c</th>
      <td>TWTTR</td>
      <td>23</td>
    </tr>
    <tr>
      <th>d</th>
      <td>GE</td>
      <td>44</td>
    </tr>
    <tr>
      <th>e</th>
      <td>MSFT</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

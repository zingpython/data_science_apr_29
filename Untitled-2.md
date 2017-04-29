

```python
# Lets calculate didvidend yield
# Dividend Yield = Annual Dividend / Current Stock Price

dividends = [1, 1.5, 1.75, 0.75, 1.25]
stock_prices = [50, 55, 62, 47, 84]
```


```python
# Dividend Yield = Annual Dividend / Current Stock Price
# can not do dividends/stock_prices
import numpy as np
```


```python
# lets convert lists into numpy arrays
# If you use different types NumPy converts everything to string
np_dividends = np.array(dividends)
np_stock_prices = np.array(stock_prices)
np_stock_prices
```




    array([50, 55, 62, 47, 84])




```python
# now we can easy perform calculations
dividend_yield = np_dividends/np_stock_prices*100
dividend_yield
```




    array([ 2.        ,  2.72727273,  2.82258065,  1.59574468,  1.48809524])




```python
# NumPy behaves differently than Python

a = [1,2,3]
b = [4,5,6]
c = a + b
c
```




    [1, 2, 3, 4, 5, 6]




```python
# NumPy adds items
b = np.array(b)
c = a + b
c
```




    array([5, 7, 9])




```python
dividend_yield[1]
```




    2.7272727272727271




```python
# values greater than 2.72
dividend_yield > 2.72
```




    array([False,  True,  True, False, False], dtype=bool)




```python
# or you could get the actual values
dividend_yield[dividend_yield > 2.72]
```




    array([ 2.72727273,  2.82258065])




```python
# 2D NumPy Arrays
# ndarray stands for N-dimensional array
type(np_dividends)
```




    numpy.ndarray




```python
# we can create 2d array from a regular python list of lists
np_2d = np.array([[1, 1.5, 1.75, 0.75, 1.25],[50, 55, 62, 47, 84]])
np_2d
```




    array([[  1.  ,   1.5 ,   1.75,   0.75,   1.25],
           [ 50.  ,  55.  ,  62.  ,  47.  ,  84.  ]])




```python
# we got rectangular data structure
# lets see how many rows and colums using shape
np_2d.shape
```




    (2, 5)




```python
# with a 2d array we can do indexing 
np_2d[1]
```




    array([ 50.,  55.,  62.,  47.,  84.])




```python
np_2d[1][1]
```




    55.0




```python
# or you could subsetting
# [row,column]
np_2d[1,1]
```




    55.0




```python
# or we could get entire second row
np_2d[1,:]
```




    array([ 50.,  55.,  62.,  47.,  84.])




```python
# Similarly we can use mean and median functions for the whole row 
avarage_stock_price = np.mean(np_2d[1,:])
avarage_stock_price
```




    59.600000000000001




```python
#standard diviation
sd = np.std(np_2d[1,:])
sd
```




    13.215142829345433




```python
#sum
s = np.sum(np_2d[1,:])
s
```




    298.0




```python
# generate data
# (distribution mean, standard dev., number of samples)

prices = np.round(np.random.normal(50, 0.20, 10), 2)
prices
```




    array([ 50.23,  50.15,  50.04,  49.99,  50.15,  50.13,  50.33,  50.24,
            50.05,  49.96])




```python
dividends = np.round(np.random.normal(1.25, 0.20, 10), 2)
dividends
```




    array([ 1.13,  1.56,  1.17,  1.33,  1.03,  1.17,  1.3 ,  1.3 ,  1.21,  1.17])




```python
# create two columns
portfolio = np.column_stack((prices, dividends))
portfolio
```




    array([[ 50.23,   1.13],
           [ 50.15,   1.56],
           [ 50.04,   1.17],
           [ 49.99,   1.33],
           [ 50.15,   1.03],
           [ 50.13,   1.17],
           [ 50.33,   1.3 ],
           [ 50.24,   1.3 ],
           [ 50.05,   1.21],
           [ 49.96,   1.17]])




```python
# lets check median stock price
m = np.median(portfolio[:,0])
m
```




    50.140000000000001




```python

```

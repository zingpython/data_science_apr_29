

```python
import numpy as np
import pandas as pd
```


```python
s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
s
```




    a    0.561559
    b   -0.930543
    c   -0.383838
    d   -0.530227
    e    0.942402
    dtype: float64




```python
s*(-1)
```




    a   -0.561559
    b    0.930543
    c    0.383838
    d    0.530227
    e   -0.942402
    dtype: float64




```python
s[0]
```




    0.56155936717957455




```python
s[:3]
```




    a    0.561559
    b   -0.930543
    c   -0.383838
    dtype: float64




```python
s[2:3]
```




    c   -0.383838
    dtype: float64




```python
s[[4, 3, 1]]
```




    e    0.942402
    d   -0.530227
    b   -0.930543
    dtype: float64




```python
s + 20
```




    a    20.561559
    b    19.069457
    c    19.616162
    d    19.469773
    e    20.942402
    dtype: float64




```python

```

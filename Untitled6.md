

```python
import pandas as pd
```


```python
cities = ["Philadelphia", "Boston","Baltimore", "Orlando"]
states = ["PA", "MA","MD", "FL"]
population = [1.5,0.6,0.6,2.35]
visitors = [41,19,24,66]
list_labels = ["City","State", "Population","Visitors"]
list_cols = [cities,states,population,visitors]
zipped = list(zip(list_labels, list_cols))
data = dict(zipped)
df = pd.DataFrame(data)
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Philadelphia</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Boston</td>
      <td>0.60</td>
      <td>MA</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Baltimore</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Orlando</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index = df["State"]
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>Boston</td>
      <td>0.60</td>
      <td>MA</td>
      <td>19</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>Orlando</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
    </tr>
  </tbody>
</table>
</div>




```python
# for loop and iterrows()
# Iterate over DataFrame rows as (index, Series) pairs

for st, row in df.iterrows():
    print("st",st)
    print("row",row)
```

    st PA
    row City          Philadelphia
    Population             1.5
    State                   PA
    Visitors                41
    Name: PA, dtype: object
    st MA
    row City          Boston
    Population       0.6
    State             MA
    Visitors          19
    Name: MA, dtype: object
    st MD
    row City          Baltimore
    Population          0.6
    State                MD
    Visitors             24
    Name: MD, dtype: object
    st FL
    row City          Orlando
    Population       2.35
    State              FL
    Visitors           66
    Name: FL, dtype: object



```python
# Now lets get the data we need
for st, row in df.iterrows():
    print(st + ": " + row["City"])
```

    PA: Philadelphia
    MA: Boston
    MD: Baltimore
    FL: Orlando



```python
# now lets do some math, suppose we need to count chr in City and save it in a new col
for st, row in df.iterrows():
    df.loc[st, "city_length"] = len(row["City"])
print(df)
```

                   City  Population State  Visitors  city_length
    State                                                       
    PA     Philadelphia        1.50    PA        41         12.0
    MA           Boston        0.60    MA        19          6.0
    MD        Baltimore        0.60    MD        24          9.0
    FL          Orlando        2.35    FL        66          7.0



```python
# however it is not the most efficient way to do it especially for a big data set

df["new_city_length"] = df["City"].apply(len)
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>Boston</td>
      <td>0.60</td>
      <td>MA</td>
      <td>19</td>
      <td>6.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>Orlando</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
      <td>7.0</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# filtering DataFrame 
df.new_city_length > 7
```




    State
    PA     True
    MA    False
    MD     True
    FL    False
    Name: new_city_length, dtype: bool




```python
# filtering
greater_than = df.new_city_length > 7
df[greater_than]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.5</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.6</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# or we could do
df[df.new_city_length > 7]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.5</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.6</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# we can combine filters and
df[(df.new_city_length > 7) & (df.new_city_length < 10)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.6</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# we can combine filters or
df[(df.new_city_length == 9) | (df.new_city_length >= 10)]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.5</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.6</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
# filtering a column based on another
df.City[df.new_city_length == 7]
```




    State
    FL    Orlando
    Name: City, dtype: object




```python
# modifying a column based on another
df.Visitors[df.new_city_length == 6] *= 2
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>Boston</td>
      <td>0.60</td>
      <td>MA</td>
      <td>76</td>
      <td>6.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>Orlando</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
      <td>7.0</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# creating methods within DataFrames
def hundreds(n):
    return n/100

df["Visitors"].apply(hundreds)

```




    State
    PA    0.41
    MA    0.76
    MD    0.24
    FL    0.66
    Name: Visitors, dtype: float64




```python
# same result with lambda function
df["Visitors"].apply(lambda n: n/100)
```




    State
    PA    0.41
    MA    0.76
    MD    0.24
    FL    0.66
    Name: Visitors, dtype: float64




```python
# now we can store this data
df["Visitors/hundreds"] = df.Visitors.apply(lambda n: n/100)
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
      <th>Visitors/hundreds</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>Philadelphia</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
      <td>0.41</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>Boston</td>
      <td>0.60</td>
      <td>MA</td>
      <td>76</td>
      <td>6.0</td>
      <td>6</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>Baltimore</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
      <td>0.24</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>Orlando</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
      <td>7.0</td>
      <td>7</td>
      <td>0.66</td>
    </tr>
  </tbody>
</table>
</div>




```python
# manipulating strings
df.City = df.City.str.upper()
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
      <th>Visitors/hundreds</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>PHILADELPHIA</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
      <td>0.41</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>BOSTON</td>
      <td>0.60</td>
      <td>MA</td>
      <td>76</td>
      <td>6.0</td>
      <td>6</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>BALTIMORE</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
      <td>0.24</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>ORLANDO</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
      <td>7.0</td>
      <td>7</td>
      <td>0.66</td>
    </tr>
  </tbody>
</table>
</div>




```python
# columns calculations
df["Total_poulation"] = df.Population + df.Visitors
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Population</th>
      <th>State</th>
      <th>Visitors</th>
      <th>city_length</th>
      <th>new_city_length</th>
      <th>Visitors/hundreds</th>
      <th>Total_poulation</th>
    </tr>
    <tr>
      <th>State</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PA</th>
      <td>PHILADELPHIA</td>
      <td>1.50</td>
      <td>PA</td>
      <td>41</td>
      <td>12.0</td>
      <td>12</td>
      <td>0.41</td>
      <td>42.50</td>
    </tr>
    <tr>
      <th>MA</th>
      <td>BOSTON</td>
      <td>0.60</td>
      <td>MA</td>
      <td>76</td>
      <td>6.0</td>
      <td>6</td>
      <td>0.76</td>
      <td>76.60</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>BALTIMORE</td>
      <td>0.60</td>
      <td>MD</td>
      <td>24</td>
      <td>9.0</td>
      <td>9</td>
      <td>0.24</td>
      <td>24.60</td>
    </tr>
    <tr>
      <th>FL</th>
      <td>ORLANDO</td>
      <td>2.35</td>
      <td>FL</td>
      <td>66</td>
      <td>7.0</td>
      <td>7</td>
      <td>0.66</td>
      <td>68.35</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

```python
import pandas as pd
import numpy as np
```


```python
#1
```


```python

    list1 = []

    df = pd.read_csv('mpg.csv')
    
    df = np.array(df)
    
    #print(df)
    
    for rows in df:
    
        if('auto' in rows[5]):
            {
                list1.append('auto')
            }
        else:
            {
                list1.append('manual')
            }
        
    df = pd.DataFrame(df)
    
    list1 = pd.DataFrame(list1)
    
    df['gear'] = list1

    print(df)
```

                  0       1    2     3  4           5  6   7   8  9       10  \
    0          audi      a4  1.8  1999  4    auto(l5)  f  18  29  p  compact   
    1          audi      a4  1.8  1999  4  manual(m5)  f  21  29  p  compact   
    2          audi      a4    2  2008  4  manual(m6)  f  20  31  p  compact   
    3          audi      a4    2  2008  4    auto(av)  f  21  30  p  compact   
    4          audi      a4  2.8  1999  6    auto(l5)  f  16  26  p  compact   
    ..          ...     ...  ...   ... ..         ... ..  ..  .. ..      ...   
    229  volkswagen  passat    2  2008  4    auto(s6)  f  19  28  p  midsize   
    230  volkswagen  passat    2  2008  4  manual(m6)  f  21  29  p  midsize   
    231  volkswagen  passat  2.8  1999  6    auto(l5)  f  16  26  p  midsize   
    232  volkswagen  passat  2.8  1999  6  manual(m5)  f  18  26  p  midsize   
    233  volkswagen  passat  3.6  2008  6    auto(s6)  f  17  26  p  midsize   
    
           gear  
    0      auto  
    1    manual  
    2    manual  
    3      auto  
    4      auto  
    ..      ...  
    229    auto  
    230  manual  
    231    auto  
    232  manual  
    233    auto  
    
    [234 rows x 12 columns]
    


```python
#2
```


```python
    df = pd.read_csv('mpg.csv')
    
    df = np.array(df)
    
    #print(df)
    
    list1 = []
    
    for rows in df:
    
        if(rows[0] in rows[1]):
            
                y = rows[1].replace(rows[0],'')
                rows[1] = y
            
        
    df = pd.DataFrame(df)
    
    #print(list1)

    print(df.loc[[202]])
```

             0            1    2     3  4           5  6   7   8  9       10
    202  toyota   tacoma 4wd  2.7  2008  4  manual(m5)  4  17  22  r  pickup
    


```python
 def manufacturer_model(a: str) -> np.array:
        
        df = pd.read_csv('mpg.csv')

        grouped_df = df.groupby("manufacturer")

        grouped_lists = grouped_df["model"].apply(list)

        grouped_lists = grouped_lists.reset_index()
        
        l = np.array(grouped_lists)
        
        a = np.where(l == a)
        
        a = np.array(a)
        
        #y = np.array(l[a])
        
        y = l[a[0]][0][1]
        
        return y
```


```python
x = manufacturer_model('audi')
print(x)
```

    ['a4', 'a4', 'a4', 'a4', 'a4', 'a4', 'a4', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a4 quattro', 'a6 quattro', 'a6 quattro', 'a6 quattro']
    

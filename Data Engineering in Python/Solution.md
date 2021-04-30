```python
import pandas as pd

df = pd.read_csv('RaCA_samples.csv', header = 0)

df1 = df[['rcasiteid','TOP','BOT','Bulkdensity','SOC_pred1', 'BDmeasured', 'BDmethod', 'Texture', 'fragvolc', 'c_tot_ncs',
'n_tot_ncs', 's_tot_ncs', 'caco3', 'Measure_BD', 'upedonid']]

df2 = pd.read_csv('RaCA_SOC_pedons.csv')
df3 = df2[['upedonid','SOCstock5', 'SOCstock30', 'SOCstock100']]

location = pd.read_csv('RaCa_general_location.csv')

location.columns = ['rcasiteid','Gen_lat','Gen_long']

mergedData = df1.merge(df3, on = 'upedonid')

DatawithLocation = mergedData.merge(location, on = 'rcasiteid')

DatawithLocation = DatawithLocation.drop_duplicates()

finalData = DatawithLocation

```

    30408
      rcasiteid   TOP    BOT  Bulkdensity  SOC_pred1 BDmeasured BDmethod Texture  \
    0  C0101F01   0.0    5.0     0.881002  49.674091    modeled      NaN      PM   
    1  C0101F01   5.0   22.0     0.881002  49.674091    modeled      NaN      PM   
    2  C0101F01  22.0  100.0     0.967665  55.530000    modeled      NaN      PM   
    3  C0101W01   0.0    5.0     0.918831  29.594032    modeled      NaN    None   
    4  C0101W01   5.0   25.0     0.904953  48.090000    modeled      NaN      PM   
    
       fragvolc  c_tot_ncs  n_tot_ncs  s_tot_ncs  caco3  Measure_BD    upedonid  \
    0       0.0  48.094150   2.401340   0.187482    NaN         NaN  C0101F01-1   
    1       0.0  50.142574   1.621640   0.095915    NaN         NaN  C0101F01-1   
    2       0.0  55.529768   1.177027   0.031538    NaN         NaN  C0101F01-1   
    3       0.0  50.992633   3.230560   0.320330    NaN         NaN  C0101W01-1   
    4       0.0  48.089204   2.929916   0.106421    NaN         NaN  C0101W01-1   
    
        SOCstock5   SOCstock30  SOCstock100  Gen_lat  Gen_long  
    0  169.511025  1076.864591  3805.801642    47.01   -122.77  
    1  169.511025  1076.864591  3805.801642    47.01   -122.77  
    2  169.511025  1076.864591  3805.801642    47.01   -122.77  
    3  338.654705  1205.698308  3853.560256    47.59   -122.19  
    4  338.654705  1205.698308  3853.560256    47.59   -122.19  
    


```python
#compiled dataset head

print(finalData.head())

```


```python
#summary
print(finalData.describe())

```

                    TOP           BOT   Bulkdensity     SOC_pred1      fragvolc  \
    count  30404.000000  30403.000000  30400.000000  30403.000000  30402.000000   
    mean      32.254144     55.867217      1.250137      4.617085      5.489178   
    std       37.039235     49.533229      0.292464      9.323602     13.320023   
    min        0.000000      1.000000      0.060216      0.001437      0.000000   
    25%        5.000000     14.000000      1.117568      0.734552      0.000000   
    50%       19.000000     44.000000      1.309481      1.462539      0.000000   
    75%       52.000000     90.000000      1.440759      3.084759      3.000000   
    max      221.000000    261.000000      1.980951     78.450000    100.000000   
    
              c_tot_ncs     n_tot_ncs     s_tot_ncs         caco3    Measure_BD  \
    count  27143.000000  27143.000000  27143.000000  15887.000000  17078.000000   
    mean       3.901650      0.226737      0.052355      5.119674      1.252646   
    std        9.086786      0.399509      0.351769     10.377672      0.293329   
    min        0.001000      0.000000      0.000000     -0.846048      0.064186   
    25%        0.491984      0.056205      0.000000      0.153638      1.097613   
    50%        1.234691      0.109150      0.010048      0.321159      1.295090   
    75%        2.798176      0.208126      0.025292      5.036177      1.458405   
    max       65.046534      4.118524     17.895758    100.225053      1.980951   
    
              SOCstock5    SOCstock30   SOCstock100       Gen_lat      Gen_long  
    count  30362.000000  30198.000000  28899.000000  30404.000000  30404.000000  
    mean      30.646445     93.500598    171.139917     39.213480    -97.217622  
    std       42.614010    136.596859    367.671538      5.136728     14.508501  
    min        0.033385      0.178608      0.178608     25.520000   -124.650000  
    25%        8.537741     33.286364     56.126791     35.400000   -109.480000  
    50%       15.229822     54.290781     90.762395     39.290000    -95.980000  
    75%       28.755454     93.437878    152.330705     43.260000    -85.250000  
    max      402.295670   1268.243420   4114.177873     48.980000    -67.150000  
    


```python

```

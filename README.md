```python
# import libraries
import numpy as np
import pandas as pd
import seaborn as sns
```


```python
df_StudentScores=pd.read_csv('StudentScores.csv')
df_StudentScores.head()
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
      <th>school_year</th>
      <th>ISDcode</th>
      <th>ISDname</th>
      <th>district_code</th>
      <th>district_name</th>
      <th>building_code</th>
      <th>building_name</th>
      <th>grade</th>
      <th>subject_name</th>
      <th>subgroup</th>
      <th>number_tested</th>
      <th>level1_highlyproficient</th>
      <th>level2_proficient</th>
      <th>level3_notproficient</th>
      <th>level4_notproficient</th>
      <th>percent_proficient</th>
      <th>average_scaled_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3580</td>
      <td>1.5</td>
      <td>13.2</td>
      <td>17.6</td>
      <td>67.8</td>
      <td>0.146</td>
      <td>314.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>American Indian or Alaska Native</td>
      <td>13</td>
      <td>0</td>
      <td>30.8</td>
      <td>0</td>
      <td>69.2</td>
      <td>0.308</td>
      <td>320.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>Asian</td>
      <td>32</td>
      <td>6.3</td>
      <td>40.6</td>
      <td>9.4</td>
      <td>43.8</td>
      <td>0.469</td>
      <td>329.97</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>Economically Disadvantaged</td>
      <td>3191</td>
      <td>1.3</td>
      <td>12.6</td>
      <td>17.6</td>
      <td>68.5</td>
      <td>0.139</td>
      <td>313.95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>English Language Learners</td>
      <td>556</td>
      <td>1.3</td>
      <td>11.5</td>
      <td>18.5</td>
      <td>68.7</td>
      <td>0.128</td>
      <td>315.46</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_StudentScores.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 9213 entries, 0 to 9212
    Data columns (total 17 columns):
     #   Column                   Non-Null Count  Dtype  
    ---  ------                   --------------  -----  
     0   school_year              9213 non-null   object 
     1   ISDcode                  9213 non-null   int64  
     2   ISDname                  9213 non-null   object 
     3   district_code            9213 non-null   int64  
     4   district_name            9213 non-null   object 
     5   building_code            8960 non-null   float64
     6   building_name            9213 non-null   object 
     7   grade                    9213 non-null   int64  
     8   subject_name             9213 non-null   object 
     9   subgroup                 9213 non-null   object 
     10  number_tested            9213 non-null   object 
     11  level1_highlyproficient  9213 non-null   object 
     12  level2_proficient        9213 non-null   object 
     13  level3_notproficient     9213 non-null   object 
     14  level4_notproficient     9213 non-null   object 
     15  percent_proficient       9213 non-null   object 
     16  average_scaled_score     9213 non-null   object 
    dtypes: float64(1), int64(3), object(13)
    memory usage: 1.2+ MB
    

#### I noticed that 'number_tested', 'level1_highlyproficient', 'level2_proficient', 'level3_notproficient', 'level4_notproficient', 'percent_proficient', 'average_scaled_score' are of type 'object', while they're supposed to be numbers.




```python
df_StudentScores.number_tested.unique()
```




    array(['3580', '13', '32', '3191', '556', '2882', '545', '1747', '1833',
           '389', '3024', '11', '97', '263', '267', '10', '3043', '< 10',
           '1841', '1753', '536', '391', '3203', '551', '29', '2908', '3594',
           '3316', '46', '2905', '2704', '522', '1646', '486', '1670', '411',
           '2794', '63', '246', '249', '2803', '1668', '1650', '408', '478',
           '2910', '515', '43', '2717', '3318', '3320', '483', '518', '2714',
           '410', '2802', '247', '274', '99', '2804', '425', '1651', '1672',
           '485', '519', '2682', '2898', '3323', '2690', '41', '2904', '509',
           '477', '1648', '416', '2811', '101', '275', '105', '2925', '448',
           '1742', '424', '1722', '505', '2797', '539', '3016', '3464',
           '3225', '57', '2806', '468', '2666', '436', '1616', '1609', '320',
           '419', '2757', '61', '62', '323', '2771', '418', '1617', '434',
           '2677', '2815', '462', '55', '3233', '3346', '54', '475', '2912',
           '1660', '1686', '2871', '67', '457', '350', '2697', '422', '1565',
           '379', '1521', '2579', '2664', '3086', '3091', '2670', '381', '53',
           '2595', '378', '1528', '1563', '421', '2710', '351', '359', '1529',
           '1566', '377', '2599', '2674', '3095', '16', '2518', '60', '366',
           '2572', '1479', '1545', '321', '362', '2658', '506', '364', '2683',
           '1551', '1489', '315', '2602', '2531', '357', '3040', '3152',
           '2631', '372', '2694', '1595', '324', '521', '1557', '2780', '498',
           '453', '58', '3455', '1786', '671', '318', '2004', '3337', '335',
           '3119', '72', '3790', '82', '76', '81', '42', '40', '80', '75',
           '38', '65', '27', '68', '39', '66', '59', '28', '31', '69', '23',
           '44', '64', '77', '74', '50', '20', '95', '84', '49', '19', '96',
           '85', '92', '87', '90', '17', '100', '98', '25', '26', '30', '56',
           '33', '15', '18', '14', '45', '48', '47', '22', '52', '24', '35',
           '34', '37', '36', '143', '131', '140', '78', '12', '141', '21',
           '73', '51', '118', '94', '104', '117', '93', '103', '86', '71',
           '70', '764', '572', '665', '346', '192', '704', '79', '91', '102',
           '83', '135', '120', '134', '126', '136', '132', '112', '110',
           '115', '113', '441', '369', '438', '231', '210', '440', '401',
           '329', '398', '206', '195', '88', '89', '119', '151', '123', '152',
           '124', '157', '130', '182', '203', '202', '106', '108', '133',
           '107', '368', '331', '250', '273', '186', '385', '265', '233',
           '384', '176', '175', '144', '164', '147', '145', '137', '142',
           '155', '260', '248', '257', '156', '258', '109', '111', '125',
           '154', '165'], dtype=object)



#### The reason is that the string '< 10' is among the values of the above fields




```python
df_EducatorEffectiveness=pd.read_csv('EducatorEffectivenessSnapshot.csv', skiprows=6)
df_EducatorEffectiveness.head()
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
      <th>location</th>
      <th>school_year</th>
      <th>highly_effective</th>
      <th>highly_effective_percent</th>
      <th>effective</th>
      <th>effective_percent</th>
      <th>minimally_effective</th>
      <th>minimally_effective_percent</th>
      <th>ineffective</th>
      <th>ineffective_percent</th>
      <th>effective_or_more_percent</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Detroit City School District</td>
      <td>2013-14</td>
      <td>2542.0</td>
      <td>0.79</td>
      <td>541.0</td>
      <td>0.17</td>
      <td>73.0</td>
      <td>0.02</td>
      <td>52.0</td>
      <td>0.02</td>
      <td>0.96</td>
      <td>3208.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Statewide</td>
      <td>2013-14</td>
      <td>36384.0</td>
      <td>0.38</td>
      <td>56814.0</td>
      <td>0.59</td>
      <td>2168.0</td>
      <td>0.02</td>
      <td>519.0</td>
      <td>0.01</td>
      <td>0.97</td>
      <td>95885.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Academy of The Americas</td>
      <td>2013-14</td>
      <td>30.0</td>
      <td>0.83</td>
      <td>5.0</td>
      <td>0.14</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.97</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Administrative Unit</td>
      <td>2013-14</td>
      <td>31.0</td>
      <td>0.65</td>
      <td>17.0</td>
      <td>0.35</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>48.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ann Arbor Trail Magnet School</td>
      <td>2013-14</td>
      <td>23.0</td>
      <td>0.92</td>
      <td>2.0</td>
      <td>0.08</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>25.0</td>
    </tr>
  </tbody>
</table>
</div>



* The rows where the 'subgroup' and 'subject_name' columns have values of 'All Students' and 'Mathematics' respectively are the rows that we should consider in our analysis.



```python
df_StudentScores[(df_StudentScores['subject_name']=='Mathematics') & (df_StudentScores['subgroup']=='All Students')]
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
      <th>school_year</th>
      <th>ISDcode</th>
      <th>ISDname</th>
      <th>district_code</th>
      <th>district_name</th>
      <th>building_code</th>
      <th>building_name</th>
      <th>grade</th>
      <th>subject_name</th>
      <th>subgroup</th>
      <th>number_tested</th>
      <th>level1_highlyproficient</th>
      <th>level2_proficient</th>
      <th>level3_notproficient</th>
      <th>level4_notproficient</th>
      <th>percent_proficient</th>
      <th>average_scaled_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3580</td>
      <td>1.5</td>
      <td>13.2</td>
      <td>17.6</td>
      <td>67.8</td>
      <td>0.146</td>
      <td>314.41</td>
    </tr>
    <tr>
      <th>29</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>4</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3316</td>
      <td>1.4</td>
      <td>15.8</td>
      <td>14</td>
      <td>68.8</td>
      <td>0.172</td>
      <td>412.41</td>
    </tr>
    <tr>
      <th>87</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>5</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3323</td>
      <td>0.5</td>
      <td>15</td>
      <td>15.4</td>
      <td>69.1</td>
      <td>0.154</td>
      <td>507.18</td>
    </tr>
    <tr>
      <th>116</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>6</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3225</td>
      <td>1.1</td>
      <td>13.7</td>
      <td>13.2</td>
      <td>72</td>
      <td>0.148</td>
      <td>604.74</td>
    </tr>
    <tr>
      <th>168</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>7</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3086</td>
      <td>0.7</td>
      <td>11.1</td>
      <td>18.8</td>
      <td>69.4</td>
      <td>0.118</td>
      <td>706.06</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9090</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>9992.0</td>
      <td>Clark, J.E. Preparatory Academy</td>
      <td>4</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>52</td>
      <td>0</td>
      <td>15.4</td>
      <td>23.1</td>
      <td>61.5</td>
      <td>0.154</td>
      <td>415.12</td>
    </tr>
    <tr>
      <th>9114</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>9992.0</td>
      <td>Clark, J.E. Preparatory Academy</td>
      <td>5</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>57</td>
      <td>0</td>
      <td>5.3</td>
      <td>5.3</td>
      <td>89.5</td>
      <td>0.053</td>
      <td>500.04</td>
    </tr>
    <tr>
      <th>9138</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>9992.0</td>
      <td>Clark, J.E. Preparatory Academy</td>
      <td>6</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>72</td>
      <td>0</td>
      <td>2.8</td>
      <td>5.6</td>
      <td>91.7</td>
      <td>0.028</td>
      <td>594.67</td>
    </tr>
    <tr>
      <th>9162</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>9992.0</td>
      <td>Clark, J.E. Preparatory Academy</td>
      <td>7</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>100</td>
      <td>0</td>
      <td>4</td>
      <td>12</td>
      <td>84</td>
      <td>0.04</td>
      <td>698.75</td>
    </tr>
    <tr>
      <th>9189</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>9992.0</td>
      <td>Clark, J.E. Preparatory Academy</td>
      <td>8</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>100</td>
      <td>0</td>
      <td>5</td>
      <td>16</td>
      <td>79</td>
      <td>0.05</td>
      <td>794.88</td>
    </tr>
  </tbody>
</table>
<p>350 rows × 17 columns</p>
</div>



* The rows where the 'building_name' column has the value 'All Buildings' are accumulative rows having the sum of the values of all schools. We should exclude these rows from our analysis, since we need the per-school statistics.


```python
df_StudentScores[(df_StudentScores['subject_name']=='Mathematics') & (df_StudentScores['subgroup']=='All Students') & (df_StudentScores['building_name']=='All Buildings')]
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
      <th>school_year</th>
      <th>ISDcode</th>
      <th>ISDname</th>
      <th>district_code</th>
      <th>district_name</th>
      <th>building_code</th>
      <th>building_name</th>
      <th>grade</th>
      <th>subject_name</th>
      <th>subgroup</th>
      <th>number_tested</th>
      <th>level1_highlyproficient</th>
      <th>level2_proficient</th>
      <th>level3_notproficient</th>
      <th>level4_notproficient</th>
      <th>percent_proficient</th>
      <th>average_scaled_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3580</td>
      <td>1.5</td>
      <td>13.2</td>
      <td>17.6</td>
      <td>67.8</td>
      <td>0.146</td>
      <td>314.41</td>
    </tr>
    <tr>
      <th>29</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>4</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3316</td>
      <td>1.4</td>
      <td>15.8</td>
      <td>14</td>
      <td>68.8</td>
      <td>0.172</td>
      <td>412.41</td>
    </tr>
    <tr>
      <th>87</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>5</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3323</td>
      <td>0.5</td>
      <td>15</td>
      <td>15.4</td>
      <td>69.1</td>
      <td>0.154</td>
      <td>507.18</td>
    </tr>
    <tr>
      <th>116</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>6</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3225</td>
      <td>1.1</td>
      <td>13.7</td>
      <td>13.2</td>
      <td>72</td>
      <td>0.148</td>
      <td>604.74</td>
    </tr>
    <tr>
      <th>168</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>7</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3086</td>
      <td>0.7</td>
      <td>11.1</td>
      <td>18.8</td>
      <td>69.4</td>
      <td>0.118</td>
      <td>706.06</td>
    </tr>
    <tr>
      <th>198</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>NaN</td>
      <td>All Buildings</td>
      <td>8</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>3024</td>
      <td>1.8</td>
      <td>10.4</td>
      <td>17.5</td>
      <td>70.3</td>
      <td>0.122</td>
      <td>801.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
# This dataframe includes all the rows with 'subject_name' of 'Mathematics', 'subgroup' of 'All Students'
# It excludes the rows having 'All Buildings' as 'buildingName', and those having '< 10' as 'number_tested'
df_StudentScores_maths_school=df_StudentScores[(df_StudentScores['subject_name']=='Mathematics') & (df_StudentScores['subgroup']=='All Students') & (df_StudentScores['building_name']!='All Buildings') & (df_StudentScores['number_tested']!='< 10')]#['number_tested'].unique()
df_StudentScores_maths_school.head()
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
      <th>school_year</th>
      <th>ISDcode</th>
      <th>ISDname</th>
      <th>district_code</th>
      <th>district_name</th>
      <th>building_code</th>
      <th>building_name</th>
      <th>grade</th>
      <th>subject_name</th>
      <th>subgroup</th>
      <th>number_tested</th>
      <th>level1_highlyproficient</th>
      <th>level2_proficient</th>
      <th>level3_notproficient</th>
      <th>level4_notproficient</th>
      <th>percent_proficient</th>
      <th>average_scaled_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>253</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>82</td>
      <td>0</td>
      <td>6.1</td>
      <td>11</td>
      <td>82.9</td>
      <td>0.061</td>
      <td>306.16</td>
    </tr>
    <tr>
      <th>272</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>4</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>65</td>
      <td>0</td>
      <td>7.7</td>
      <td>12.3</td>
      <td>80</td>
      <td>0.077</td>
      <td>404.63</td>
    </tr>
    <tr>
      <th>304</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>5</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>58</td>
      <td>0</td>
      <td>5.2</td>
      <td>3.4</td>
      <td>91.4</td>
      <td>0.052</td>
      <td>494.98</td>
    </tr>
    <tr>
      <th>328</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>6</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>69</td>
      <td>0</td>
      <td>0</td>
      <td>1.4</td>
      <td>98.6</td>
      <td>0</td>
      <td>587.99</td>
    </tr>
    <tr>
      <th>361</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>7</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>95</td>
      <td>0</td>
      <td>6.3</td>
      <td>11.6</td>
      <td>82.1</td>
      <td>0.063</td>
      <td>698.83</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Here I convert the 'number_stated', 'level1_highlyproficient', and 'level2_proficient' to number formats.
# I also added a new column to calculate the number of level1 & level2 students in each school/grade.
df_StudentScores_maths_school['number_tested']=df_StudentScores_maths_school['number_tested'].astype(int)
df_StudentScores_maths_school['level1_highlyproficient']=df_StudentScores_maths_school['level1_highlyproficient'].astype(float)
df_StudentScores_maths_school['level2_proficient']=df_StudentScores_maths_school['level2_proficient'].astype(float)
df_StudentScores_maths_school['proficient_and_higher']=(df_StudentScores_maths_school['number_tested']*(df_StudentScores_maths_school['level1_highlyproficient']+df_StudentScores_maths_school['level2_proficient'])/100).apply(np.round).astype(int)
df_StudentScores_maths_school.head()
```

    c:\users\hedey\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      This is separate from the ipykernel package so we can avoid doing imports until
    c:\users\hedey\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      after removing the cwd from sys.path.
    c:\users\hedey\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """
    c:\users\hedey\appdata\local\programs\python\python37\lib\site-packages\ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      
    




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
      <th>school_year</th>
      <th>ISDcode</th>
      <th>ISDname</th>
      <th>district_code</th>
      <th>district_name</th>
      <th>building_code</th>
      <th>building_name</th>
      <th>grade</th>
      <th>subject_name</th>
      <th>subgroup</th>
      <th>number_tested</th>
      <th>level1_highlyproficient</th>
      <th>level2_proficient</th>
      <th>level3_notproficient</th>
      <th>level4_notproficient</th>
      <th>percent_proficient</th>
      <th>average_scaled_score</th>
      <th>proficient_and_higher</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>253</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>3</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>82</td>
      <td>0.0</td>
      <td>6.1</td>
      <td>11</td>
      <td>82.9</td>
      <td>0.061</td>
      <td>306.16</td>
      <td>5</td>
    </tr>
    <tr>
      <th>272</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>4</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>65</td>
      <td>0.0</td>
      <td>7.7</td>
      <td>12.3</td>
      <td>80</td>
      <td>0.077</td>
      <td>404.63</td>
      <td>5</td>
    </tr>
    <tr>
      <th>304</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>5</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>58</td>
      <td>0.0</td>
      <td>5.2</td>
      <td>3.4</td>
      <td>91.4</td>
      <td>0.052</td>
      <td>494.98</td>
      <td>3</td>
    </tr>
    <tr>
      <th>328</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>6</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>69</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.4</td>
      <td>98.6</td>
      <td>0</td>
      <td>587.99</td>
      <td>0</td>
    </tr>
    <tr>
      <th>361</th>
      <td>13 - 14 School Year</td>
      <td>82</td>
      <td>Wayne RESA</td>
      <td>82010</td>
      <td>Detroit City School District</td>
      <td>4.0</td>
      <td>Henderson Academy</td>
      <td>7</td>
      <td>Mathematics</td>
      <td>All Students</td>
      <td>95</td>
      <td>0.0</td>
      <td>6.3</td>
      <td>11.6</td>
      <td>82.1</td>
      <td>0.063</td>
      <td>698.83</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



#### Here is how the first 10 rows of data will look like if I grouped by 'building_name' and 'grade'


```python
df_StudentScores_maths_school.groupby(['building_name','grade']).sum()[['number_tested', 'proficient_and_higher']].head(10)
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
      <th></th>
      <th>number_tested</th>
      <th>proficient_and_higher</th>
    </tr>
    <tr>
      <th>building_name</th>
      <th>grade</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="6" valign="top">Academy of The Americas</th>
      <th>3</th>
      <td>82</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>74</td>
      <td>13</td>
    </tr>
    <tr>
      <th>5</th>
      <td>82</td>
      <td>13</td>
    </tr>
    <tr>
      <th>6</th>
      <td>74</td>
      <td>9</td>
    </tr>
    <tr>
      <th>7</th>
      <td>57</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>64</td>
      <td>9</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">Ann Arbor Trail Magnet School</th>
      <th>3</th>
      <td>38</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>51</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>52</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>38</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by 'building_name' to obtain the total 'number_tested', and 'proficient_and_higher' students per school
df_math_prof=df_StudentScores_maths_school.groupby(['building_name']).sum()[['number_tested', 'proficient_and_higher']].reset_index()
df_math_prof.head(10)
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
      <th>building_name</th>
      <th>number_tested</th>
      <th>proficient_and_higher</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Academy of The Americas</td>
      <td>433</td>
      <td>58</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ann Arbor Trail Magnet School</td>
      <td>268</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bagley Elementary School</td>
      <td>167</td>
      <td>29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bates Academy</td>
      <td>565</td>
      <td>277</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bennett Elementary School</td>
      <td>178</td>
      <td>31</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Blackwell Institute</td>
      <td>211</td>
      <td>8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bow Elementary-Middle School</td>
      <td>251</td>
      <td>32</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brewer Elementary-Middle School</td>
      <td>350</td>
      <td>53</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Brown, Ronald Academy</td>
      <td>330</td>
      <td>63</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bunche Elementary-Middle School</td>
      <td>228</td>
      <td>31</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add a column for the percentage of level1 & level2 students in each school
df_math_prof['prof_percent']=df_math_prof['proficient_and_higher']/df_math_prof['number_tested']
df_math_prof.head(10)
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
      <th>building_name</th>
      <th>number_tested</th>
      <th>proficient_and_higher</th>
      <th>prof_percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Academy of The Americas</td>
      <td>433</td>
      <td>58</td>
      <td>0.133949</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ann Arbor Trail Magnet School</td>
      <td>268</td>
      <td>30</td>
      <td>0.111940</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bagley Elementary School</td>
      <td>167</td>
      <td>29</td>
      <td>0.173653</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bates Academy</td>
      <td>565</td>
      <td>277</td>
      <td>0.490265</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bennett Elementary School</td>
      <td>178</td>
      <td>31</td>
      <td>0.174157</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Blackwell Institute</td>
      <td>211</td>
      <td>8</td>
      <td>0.037915</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bow Elementary-Middle School</td>
      <td>251</td>
      <td>32</td>
      <td>0.127490</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brewer Elementary-Middle School</td>
      <td>350</td>
      <td>53</td>
      <td>0.151429</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Brown, Ronald Academy</td>
      <td>330</td>
      <td>63</td>
      <td>0.190909</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bunche Elementary-Middle School</td>
      <td>228</td>
      <td>31</td>
      <td>0.135965</td>
    </tr>
  </tbody>
</table>
</div>



### Top-10 Mathematics 'Proficint+' schools: 


```python
# Sort the table descendingly by prof_percent, and keep only the first 10 rows (Top-10 schools)
df_math_prof_top_ten=df_math_prof.sort_values('prof_percent', ascending=False).iloc[:10,:]
df_math_prof_top_ten.reset_index(drop=True, inplace=True)
df_math_prof_top_ten
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
      <th>building_name</th>
      <th>number_tested</th>
      <th>proficient_and_higher</th>
      <th>prof_percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wright, Charles School</td>
      <td>179</td>
      <td>112</td>
      <td>0.625698</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chrysler Elementary School</td>
      <td>92</td>
      <td>52</td>
      <td>0.565217</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bates Academy</td>
      <td>565</td>
      <td>277</td>
      <td>0.490265</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Davison Elementary-Middle School</td>
      <td>434</td>
      <td>199</td>
      <td>0.458525</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Burton International School</td>
      <td>364</td>
      <td>134</td>
      <td>0.368132</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dixon Elementary School</td>
      <td>476</td>
      <td>169</td>
      <td>0.355042</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Pasteur Elementary School</td>
      <td>163</td>
      <td>43</td>
      <td>0.263804</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Greenfield Union Elementary-Middle School</td>
      <td>155</td>
      <td>38</td>
      <td>0.245161</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Thirkell Elementary School</td>
      <td>255</td>
      <td>60</td>
      <td>0.235294</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Cooke Elementary School</td>
      <td>179</td>
      <td>41</td>
      <td>0.229050</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Export the dataframe to a .csv file
df_math_prof_top_ten.to_csv('top_10_maths_pro_schools.csv', index=False)
```

### Relationship between Maths proficiency and Educator effectiveness:


```python
# Now, I'll merge the df_math_prof with the df_EducatorEffectiveness to explore the relationship between Maths proficincy and educator effectiveness
df_math_prof_effectiveness=df_math_prof.merge(df_EducatorEffectiveness, left_on='building_name', right_on='location', how='inner')
df_math_prof_effectiveness.head(10)
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
      <th>building_name</th>
      <th>number_tested</th>
      <th>proficient_and_higher</th>
      <th>prof_percent</th>
      <th>location</th>
      <th>school_year</th>
      <th>highly_effective</th>
      <th>highly_effective_percent</th>
      <th>effective</th>
      <th>effective_percent</th>
      <th>minimally_effective</th>
      <th>minimally_effective_percent</th>
      <th>ineffective</th>
      <th>ineffective_percent</th>
      <th>effective_or_more_percent</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Academy of The Americas</td>
      <td>433</td>
      <td>58</td>
      <td>0.133949</td>
      <td>Academy of The Americas</td>
      <td>2013-14</td>
      <td>30.0</td>
      <td>0.83</td>
      <td>5.0</td>
      <td>0.14</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.97</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ann Arbor Trail Magnet School</td>
      <td>268</td>
      <td>30</td>
      <td>0.111940</td>
      <td>Ann Arbor Trail Magnet School</td>
      <td>2013-14</td>
      <td>23.0</td>
      <td>0.92</td>
      <td>2.0</td>
      <td>0.08</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>25.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bagley Elementary School</td>
      <td>167</td>
      <td>29</td>
      <td>0.173653</td>
      <td>Bagley Elementary School</td>
      <td>2013-14</td>
      <td>15.0</td>
      <td>0.71</td>
      <td>4.0</td>
      <td>0.19</td>
      <td>2.0</td>
      <td>0.10</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.90</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bates Academy</td>
      <td>565</td>
      <td>277</td>
      <td>0.490265</td>
      <td>Bates Academy</td>
      <td>2013-14</td>
      <td>38.0</td>
      <td>0.97</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bennett Elementary School</td>
      <td>178</td>
      <td>31</td>
      <td>0.174157</td>
      <td>Bennett Elementary School</td>
      <td>2013-14</td>
      <td>23.0</td>
      <td>0.88</td>
      <td>3.0</td>
      <td>0.12</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Blackwell Institute</td>
      <td>211</td>
      <td>8</td>
      <td>0.037915</td>
      <td>Blackwell Institute</td>
      <td>2013-14</td>
      <td>16.0</td>
      <td>0.57</td>
      <td>10.0</td>
      <td>0.36</td>
      <td>2.0</td>
      <td>0.07</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.93</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bow Elementary-Middle School</td>
      <td>251</td>
      <td>32</td>
      <td>0.127490</td>
      <td>Bow Elementary-Middle School</td>
      <td>2013-14</td>
      <td>19.0</td>
      <td>0.56</td>
      <td>14.0</td>
      <td>0.41</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.97</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brewer Elementary-Middle School</td>
      <td>350</td>
      <td>53</td>
      <td>0.151429</td>
      <td>Brewer Elementary-Middle School</td>
      <td>2013-14</td>
      <td>25.0</td>
      <td>0.81</td>
      <td>4.0</td>
      <td>0.13</td>
      <td>2.0</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.94</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Brown, Ronald Academy</td>
      <td>330</td>
      <td>63</td>
      <td>0.190909</td>
      <td>Brown, Ronald Academy</td>
      <td>2013-14</td>
      <td>36.0</td>
      <td>0.80</td>
      <td>8.0</td>
      <td>0.18</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.98</td>
      <td>45.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bunche Elementary-Middle School</td>
      <td>228</td>
      <td>31</td>
      <td>0.135965</td>
      <td>Bunche Elementary-Middle School</td>
      <td>2013-14</td>
      <td>37.0</td>
      <td>0.90</td>
      <td>2.0</td>
      <td>0.05</td>
      <td>1.0</td>
      <td>0.03</td>
      <td>1.0</td>
      <td>0.02</td>
      <td>0.95</td>
      <td>41.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Keep only the location and percentages columns
df_percents=pd.concat([df_math_prof_effectiveness[['location']], df_math_prof_effectiveness.loc[:,df_math_prof_effectiveness.columns.str.endswith('percent')]], axis=1)
df_percents.head(10)
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
      <th>location</th>
      <th>prof_percent</th>
      <th>highly_effective_percent</th>
      <th>effective_percent</th>
      <th>minimally_effective_percent</th>
      <th>ineffective_percent</th>
      <th>effective_or_more_percent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Academy of The Americas</td>
      <td>0.133949</td>
      <td>0.83</td>
      <td>0.14</td>
      <td>0.00</td>
      <td>0.03</td>
      <td>0.97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ann Arbor Trail Magnet School</td>
      <td>0.111940</td>
      <td>0.92</td>
      <td>0.08</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bagley Elementary School</td>
      <td>0.173653</td>
      <td>0.71</td>
      <td>0.19</td>
      <td>0.10</td>
      <td>0.00</td>
      <td>0.90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bates Academy</td>
      <td>0.490265</td>
      <td>0.97</td>
      <td>0.03</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bennett Elementary School</td>
      <td>0.174157</td>
      <td>0.88</td>
      <td>0.12</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Blackwell Institute</td>
      <td>0.037915</td>
      <td>0.57</td>
      <td>0.36</td>
      <td>0.07</td>
      <td>0.00</td>
      <td>0.93</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Bow Elementary-Middle School</td>
      <td>0.127490</td>
      <td>0.56</td>
      <td>0.41</td>
      <td>0.03</td>
      <td>0.00</td>
      <td>0.97</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Brewer Elementary-Middle School</td>
      <td>0.151429</td>
      <td>0.81</td>
      <td>0.13</td>
      <td>0.06</td>
      <td>0.00</td>
      <td>0.94</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Brown, Ronald Academy</td>
      <td>0.190909</td>
      <td>0.80</td>
      <td>0.18</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.98</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Bunche Elementary-Middle School</td>
      <td>0.135965</td>
      <td>0.90</td>
      <td>0.05</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>0.95</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plot the scatter matrix to take an idea about the relationships
pd.plotting.scatter_matrix(df_percents, figsize=(15,15));
```


    
![png](https://raw.githubusercontent.com/hedeya1980/Images/main/scatter_matrix.png)
    


#### The above scatter plots don't show strong releationships between the prof_percent and the effectiveness percentages


```python
# Explore the correlation between the prof_percent, and the effectiveness percentages
sns.heatmap(df_percents.corr(), annot=True, fmt=".2f");
```


    
![png](https://raw.githubusercontent.com/hedeya1980/Images/main/corr_heatmap.png)
    


### Conclusion:

* The above correlation heatmap show a weak positive correlation between 'prof_percent' and 'highly_effective_percent' (0.2), and between 'prof_percent' and 'effective_or_more_percent' (0.23). In other words, Maths proficincy tends to increase whenever 'highly_effective_percent' and 'effective_or_more_percent' increase.
* The heatmap also shows weak negative correlations between 'prof_percent' and the 3 other effectiveness percentages: ['effective_percent' (-0.15), 'minimally_effective_percent' (-0.2), and 'ineffective_percent' (-0.13)], which suggest that Maths proficiency tends to decrease when those 3 effectivess percentages increase.




```python

```



```python
# Dependencies
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
sns.set(color_codes=True)
```


```python
# Read CSV Files
city_data_df = pd.read_csv("raw_data/city_data.csv")
ride_data_df = pd.read_csv("raw_data/ride_data.csv")
```


```python
#Initialize lists
cmap=[]
```


```python
#Check City Data
city_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Check Ride Data
ride_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Get no. of rides by city from Ride data
ride_data_city = ride_data_df.groupby("city")
city_ridecount_df = pd.DataFrame(ride_data_city["ride_id"].count())

city_ridecount_df = city_ridecount_df.rename(columns={"ride_id":"no. of rides"})
city_ridecount_df.reset_index(inplace=True)
city_ridecount_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>no. of rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>19</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>31</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>29</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>12</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Conwaymouth</td>
      <td>11</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Davidtown</td>
      <td>21</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Davistown</td>
      <td>25</td>
    </tr>
    <tr>
      <th>13</th>
      <td>East Cherylfurt</td>
      <td>13</td>
    </tr>
    <tr>
      <th>14</th>
      <td>East Douglas</td>
      <td>22</td>
    </tr>
    <tr>
      <th>15</th>
      <td>East Erin</td>
      <td>28</td>
    </tr>
    <tr>
      <th>16</th>
      <td>East Jenniferchester</td>
      <td>19</td>
    </tr>
    <tr>
      <th>17</th>
      <td>East Leslie</td>
      <td>11</td>
    </tr>
    <tr>
      <th>18</th>
      <td>East Stephen</td>
      <td>10</td>
    </tr>
    <tr>
      <th>19</th>
      <td>East Troybury</td>
      <td>7</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Edwardsbury</td>
      <td>27</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Erikport</td>
      <td>8</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Eriktown</td>
      <td>19</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Floresberg</td>
      <td>10</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Fosterside</td>
      <td>24</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Hernandezshire</td>
      <td>9</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Horneland</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Jacksonfort</td>
      <td>6</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Jacobfort</td>
      <td>31</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Jasonfort</td>
      <td>12</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>South Roy</td>
      <td>22</td>
    </tr>
    <tr>
      <th>96</th>
      <td>South Shannonborough</td>
      <td>15</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Spencertown</td>
      <td>26</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Stevensport</td>
      <td>5</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Stewartview</td>
      <td>30</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Swansonbury</td>
      <td>34</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Thomastown</td>
      <td>24</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Tiffanyton</td>
      <td>13</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Torresshire</td>
      <td>26</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Travisville</td>
      <td>23</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Vickimouth</td>
      <td>15</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Webstertown</td>
      <td>16</td>
    </tr>
    <tr>
      <th>107</th>
      <td>West Alexis</td>
      <td>20</td>
    </tr>
    <tr>
      <th>108</th>
      <td>West Brandy</td>
      <td>30</td>
    </tr>
    <tr>
      <th>109</th>
      <td>West Brittanyton</td>
      <td>24</td>
    </tr>
    <tr>
      <th>110</th>
      <td>West Dawnfurt</td>
      <td>29</td>
    </tr>
    <tr>
      <th>111</th>
      <td>West Evan</td>
      <td>12</td>
    </tr>
    <tr>
      <th>112</th>
      <td>West Jefferyfurt</td>
      <td>21</td>
    </tr>
    <tr>
      <th>113</th>
      <td>West Kevintown</td>
      <td>7</td>
    </tr>
    <tr>
      <th>114</th>
      <td>West Oscar</td>
      <td>29</td>
    </tr>
    <tr>
      <th>115</th>
      <td>West Pamelaborough</td>
      <td>14</td>
    </tr>
    <tr>
      <th>116</th>
      <td>West Paulport</td>
      <td>17</td>
    </tr>
    <tr>
      <th>117</th>
      <td>West Peter</td>
      <td>31</td>
    </tr>
    <tr>
      <th>118</th>
      <td>West Sydneyhaven</td>
      <td>18</td>
    </tr>
    <tr>
      <th>119</th>
      <td>West Tony</td>
      <td>19</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Williamchester</td>
      <td>11</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Williamshire</td>
      <td>31</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Wiseborough</td>
      <td>19</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Yolandafurt</td>
      <td>20</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Zimmermanmouth</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 2 columns</p>
</div>




```python
#Get average fare by city from Ride data
city_avgfare = ride_data_city["fare"].mean()
city_avgfare_df = pd.DataFrame(city_avgfare)
city_avgfare_df = city_avgfare_df.rename(columns={"fare":"Average Fare"})
city_avgfare_df.reset_index(inplace=True)
city_avgfare_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Average Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>25.106452</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>33.711333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>36.606000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>25.395517</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>31.051667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Conwaymouth</td>
      <td>34.591818</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Davidtown</td>
      <td>22.978095</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Davistown</td>
      <td>21.497200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>East Cherylfurt</td>
      <td>31.416154</td>
    </tr>
    <tr>
      <th>14</th>
      <td>East Douglas</td>
      <td>26.169091</td>
    </tr>
    <tr>
      <th>15</th>
      <td>East Erin</td>
      <td>24.478214</td>
    </tr>
    <tr>
      <th>16</th>
      <td>East Jenniferchester</td>
      <td>32.599474</td>
    </tr>
    <tr>
      <th>17</th>
      <td>East Leslie</td>
      <td>33.660909</td>
    </tr>
    <tr>
      <th>18</th>
      <td>East Stephen</td>
      <td>39.053000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>East Troybury</td>
      <td>33.244286</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Edwardsbury</td>
      <td>26.876667</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Erikport</td>
      <td>30.043750</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Eriktown</td>
      <td>25.478947</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Floresberg</td>
      <td>32.310000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Fosterside</td>
      <td>23.034583</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Hernandezshire</td>
      <td>32.002222</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Horneland</td>
      <td>21.482500</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Jacksonfort</td>
      <td>32.006667</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Jacobfort</td>
      <td>24.779355</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Jasonfort</td>
      <td>27.831667</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>South Roy</td>
      <td>26.031364</td>
    </tr>
    <tr>
      <th>96</th>
      <td>South Shannonborough</td>
      <td>26.516667</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Spencertown</td>
      <td>23.681154</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Stevensport</td>
      <td>31.948000</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Stewartview</td>
      <td>21.614000</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Swansonbury</td>
      <td>27.464706</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Thomastown</td>
      <td>30.308333</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Tiffanyton</td>
      <td>28.510000</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Torresshire</td>
      <td>24.207308</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Travisville</td>
      <td>27.220870</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Vickimouth</td>
      <td>21.474667</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Webstertown</td>
      <td>29.721250</td>
    </tr>
    <tr>
      <th>107</th>
      <td>West Alexis</td>
      <td>19.523000</td>
    </tr>
    <tr>
      <th>108</th>
      <td>West Brandy</td>
      <td>24.157667</td>
    </tr>
    <tr>
      <th>109</th>
      <td>West Brittanyton</td>
      <td>25.436250</td>
    </tr>
    <tr>
      <th>110</th>
      <td>West Dawnfurt</td>
      <td>22.330345</td>
    </tr>
    <tr>
      <th>111</th>
      <td>West Evan</td>
      <td>27.013333</td>
    </tr>
    <tr>
      <th>112</th>
      <td>West Jefferyfurt</td>
      <td>21.072857</td>
    </tr>
    <tr>
      <th>113</th>
      <td>West Kevintown</td>
      <td>21.528571</td>
    </tr>
    <tr>
      <th>114</th>
      <td>West Oscar</td>
      <td>24.280000</td>
    </tr>
    <tr>
      <th>115</th>
      <td>West Pamelaborough</td>
      <td>33.799286</td>
    </tr>
    <tr>
      <th>116</th>
      <td>West Paulport</td>
      <td>33.278235</td>
    </tr>
    <tr>
      <th>117</th>
      <td>West Peter</td>
      <td>24.875484</td>
    </tr>
    <tr>
      <th>118</th>
      <td>West Sydneyhaven</td>
      <td>22.368333</td>
    </tr>
    <tr>
      <th>119</th>
      <td>West Tony</td>
      <td>29.609474</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Williamchester</td>
      <td>34.278182</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Williamshire</td>
      <td>26.990323</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Wiseborough</td>
      <td>22.676842</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Yolandafurt</td>
      <td>27.205500</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Zimmermanmouth</td>
      <td>28.301667</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 2 columns</p>
</div>




```python
#Create a merged df with rides & average fare
city_ridecount_df = city_ridecount_df.merge(city_avgfare_df, on="city")
city_ridecount_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>no. of rides</th>
      <th>Average Fare_x</th>
      <th>Average Fare_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>31</td>
      <td>23.928710</td>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>26</td>
      <td>20.609615</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>9</td>
      <td>37.315556</td>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>22</td>
      <td>23.625000</td>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>19</td>
      <td>21.981579</td>
      <td>21.981579</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arnoldview</td>
      <td>31</td>
      <td>25.106452</td>
      <td>25.106452</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Campbellport</td>
      <td>15</td>
      <td>33.711333</td>
      <td>33.711333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Carrollbury</td>
      <td>10</td>
      <td>36.606000</td>
      <td>36.606000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Carrollfort</td>
      <td>29</td>
      <td>25.395517</td>
      <td>25.395517</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Clarkstad</td>
      <td>12</td>
      <td>31.051667</td>
      <td>31.051667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Conwaymouth</td>
      <td>11</td>
      <td>34.591818</td>
      <td>34.591818</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Davidtown</td>
      <td>21</td>
      <td>22.978095</td>
      <td>22.978095</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Davistown</td>
      <td>25</td>
      <td>21.497200</td>
      <td>21.497200</td>
    </tr>
    <tr>
      <th>13</th>
      <td>East Cherylfurt</td>
      <td>13</td>
      <td>31.416154</td>
      <td>31.416154</td>
    </tr>
    <tr>
      <th>14</th>
      <td>East Douglas</td>
      <td>22</td>
      <td>26.169091</td>
      <td>26.169091</td>
    </tr>
    <tr>
      <th>15</th>
      <td>East Erin</td>
      <td>28</td>
      <td>24.478214</td>
      <td>24.478214</td>
    </tr>
    <tr>
      <th>16</th>
      <td>East Jenniferchester</td>
      <td>19</td>
      <td>32.599474</td>
      <td>32.599474</td>
    </tr>
    <tr>
      <th>17</th>
      <td>East Leslie</td>
      <td>11</td>
      <td>33.660909</td>
      <td>33.660909</td>
    </tr>
    <tr>
      <th>18</th>
      <td>East Stephen</td>
      <td>10</td>
      <td>39.053000</td>
      <td>39.053000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>East Troybury</td>
      <td>7</td>
      <td>33.244286</td>
      <td>33.244286</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Edwardsbury</td>
      <td>27</td>
      <td>26.876667</td>
      <td>26.876667</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Erikport</td>
      <td>8</td>
      <td>30.043750</td>
      <td>30.043750</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Eriktown</td>
      <td>19</td>
      <td>25.478947</td>
      <td>25.478947</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Floresberg</td>
      <td>10</td>
      <td>32.310000</td>
      <td>32.310000</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Fosterside</td>
      <td>24</td>
      <td>23.034583</td>
      <td>23.034583</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Hernandezshire</td>
      <td>9</td>
      <td>32.002222</td>
      <td>32.002222</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Horneland</td>
      <td>4</td>
      <td>21.482500</td>
      <td>21.482500</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Jacksonfort</td>
      <td>6</td>
      <td>32.006667</td>
      <td>32.006667</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Jacobfort</td>
      <td>31</td>
      <td>24.779355</td>
      <td>24.779355</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Jasonfort</td>
      <td>12</td>
      <td>27.831667</td>
      <td>27.831667</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>South Roy</td>
      <td>22</td>
      <td>26.031364</td>
      <td>26.031364</td>
    </tr>
    <tr>
      <th>96</th>
      <td>South Shannonborough</td>
      <td>15</td>
      <td>26.516667</td>
      <td>26.516667</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Spencertown</td>
      <td>26</td>
      <td>23.681154</td>
      <td>23.681154</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Stevensport</td>
      <td>5</td>
      <td>31.948000</td>
      <td>31.948000</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Stewartview</td>
      <td>30</td>
      <td>21.614000</td>
      <td>21.614000</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Swansonbury</td>
      <td>34</td>
      <td>27.464706</td>
      <td>27.464706</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Thomastown</td>
      <td>24</td>
      <td>30.308333</td>
      <td>30.308333</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Tiffanyton</td>
      <td>13</td>
      <td>28.510000</td>
      <td>28.510000</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Torresshire</td>
      <td>26</td>
      <td>24.207308</td>
      <td>24.207308</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Travisville</td>
      <td>23</td>
      <td>27.220870</td>
      <td>27.220870</td>
    </tr>
    <tr>
      <th>105</th>
      <td>Vickimouth</td>
      <td>15</td>
      <td>21.474667</td>
      <td>21.474667</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Webstertown</td>
      <td>16</td>
      <td>29.721250</td>
      <td>29.721250</td>
    </tr>
    <tr>
      <th>107</th>
      <td>West Alexis</td>
      <td>20</td>
      <td>19.523000</td>
      <td>19.523000</td>
    </tr>
    <tr>
      <th>108</th>
      <td>West Brandy</td>
      <td>30</td>
      <td>24.157667</td>
      <td>24.157667</td>
    </tr>
    <tr>
      <th>109</th>
      <td>West Brittanyton</td>
      <td>24</td>
      <td>25.436250</td>
      <td>25.436250</td>
    </tr>
    <tr>
      <th>110</th>
      <td>West Dawnfurt</td>
      <td>29</td>
      <td>22.330345</td>
      <td>22.330345</td>
    </tr>
    <tr>
      <th>111</th>
      <td>West Evan</td>
      <td>12</td>
      <td>27.013333</td>
      <td>27.013333</td>
    </tr>
    <tr>
      <th>112</th>
      <td>West Jefferyfurt</td>
      <td>21</td>
      <td>21.072857</td>
      <td>21.072857</td>
    </tr>
    <tr>
      <th>113</th>
      <td>West Kevintown</td>
      <td>7</td>
      <td>21.528571</td>
      <td>21.528571</td>
    </tr>
    <tr>
      <th>114</th>
      <td>West Oscar</td>
      <td>29</td>
      <td>24.280000</td>
      <td>24.280000</td>
    </tr>
    <tr>
      <th>115</th>
      <td>West Pamelaborough</td>
      <td>14</td>
      <td>33.799286</td>
      <td>33.799286</td>
    </tr>
    <tr>
      <th>116</th>
      <td>West Paulport</td>
      <td>17</td>
      <td>33.278235</td>
      <td>33.278235</td>
    </tr>
    <tr>
      <th>117</th>
      <td>West Peter</td>
      <td>31</td>
      <td>24.875484</td>
      <td>24.875484</td>
    </tr>
    <tr>
      <th>118</th>
      <td>West Sydneyhaven</td>
      <td>18</td>
      <td>22.368333</td>
      <td>22.368333</td>
    </tr>
    <tr>
      <th>119</th>
      <td>West Tony</td>
      <td>19</td>
      <td>29.609474</td>
      <td>29.609474</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Williamchester</td>
      <td>11</td>
      <td>34.278182</td>
      <td>34.278182</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Williamshire</td>
      <td>31</td>
      <td>26.990323</td>
      <td>26.990323</td>
    </tr>
    <tr>
      <th>122</th>
      <td>Wiseborough</td>
      <td>19</td>
      <td>22.676842</td>
      <td>22.676842</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Yolandafurt</td>
      <td>20</td>
      <td>27.205500</td>
      <td>27.205500</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Zimmermanmouth</td>
      <td>24</td>
      <td>28.301667</td>
      <td>28.301667</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 4 columns</p>
</div>




```python
#Create a merged df with rides & average fare and City Data by city
final_df = city_data_df.merge(city_ridecount_df,on="city")
final_df 
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>no. of rides</th>
      <th>Average Fare_x</th>
      <th>Average Fare_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>28</td>
      <td>21.806429</td>
      <td>21.806429</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
      <td>26</td>
      <td>25.899615</td>
      <td>25.899615</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
      <td>22</td>
      <td>26.169091</td>
      <td>26.169091</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
      <td>29</td>
      <td>22.330345</td>
      <td>22.330345</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
      <td>23</td>
      <td>21.332609</td>
      <td>21.332609</td>
    </tr>
    <tr>
      <th>5</th>
      <td>South Josephville</td>
      <td>4</td>
      <td>Urban</td>
      <td>24</td>
      <td>26.823750</td>
      <td>26.823750</td>
    </tr>
    <tr>
      <th>6</th>
      <td>West Sydneyhaven</td>
      <td>70</td>
      <td>Urban</td>
      <td>18</td>
      <td>22.368333</td>
      <td>22.368333</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Travisville</td>
      <td>37</td>
      <td>Urban</td>
      <td>23</td>
      <td>27.220870</td>
      <td>27.220870</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Torresshire</td>
      <td>70</td>
      <td>Urban</td>
      <td>26</td>
      <td>24.207308</td>
      <td>24.207308</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Lisaville</td>
      <td>66</td>
      <td>Urban</td>
      <td>28</td>
      <td>28.428929</td>
      <td>28.428929</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Mooreview</td>
      <td>34</td>
      <td>Urban</td>
      <td>21</td>
      <td>29.520476</td>
      <td>29.520476</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Smithhaven</td>
      <td>67</td>
      <td>Urban</td>
      <td>27</td>
      <td>22.788889</td>
      <td>22.788889</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Carrollfort</td>
      <td>55</td>
      <td>Urban</td>
      <td>29</td>
      <td>25.395517</td>
      <td>25.395517</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Port Josephfurt</td>
      <td>28</td>
      <td>Urban</td>
      <td>22</td>
      <td>26.367727</td>
      <td>26.367727</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Lake Jeffreyland</td>
      <td>15</td>
      <td>Urban</td>
      <td>25</td>
      <td>27.334800</td>
      <td>27.334800</td>
    </tr>
    <tr>
      <th>15</th>
      <td>South Louis</td>
      <td>12</td>
      <td>Urban</td>
      <td>32</td>
      <td>27.087500</td>
      <td>27.087500</td>
    </tr>
    <tr>
      <th>16</th>
      <td>West Peter</td>
      <td>61</td>
      <td>Urban</td>
      <td>31</td>
      <td>24.875484</td>
      <td>24.875484</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Kimberlychester</td>
      <td>13</td>
      <td>Urban</td>
      <td>27</td>
      <td>22.947037</td>
      <td>22.947037</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>Urban</td>
      <td>26</td>
      <td>20.609615</td>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Sarabury</td>
      <td>46</td>
      <td>Urban</td>
      <td>27</td>
      <td>23.490000</td>
      <td>23.490000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Yolandafurt</td>
      <td>7</td>
      <td>Urban</td>
      <td>20</td>
      <td>27.205500</td>
      <td>27.205500</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Edwardsbury</td>
      <td>11</td>
      <td>Urban</td>
      <td>27</td>
      <td>26.876667</td>
      <td>26.876667</td>
    </tr>
    <tr>
      <th>22</th>
      <td>New Andreamouth</td>
      <td>42</td>
      <td>Urban</td>
      <td>28</td>
      <td>24.966786</td>
      <td>24.966786</td>
    </tr>
    <tr>
      <th>23</th>
      <td>New David</td>
      <td>31</td>
      <td>Urban</td>
      <td>28</td>
      <td>27.084286</td>
      <td>27.084286</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Arnoldview</td>
      <td>41</td>
      <td>Urban</td>
      <td>31</td>
      <td>25.106452</td>
      <td>25.106452</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Williamshire</td>
      <td>70</td>
      <td>Urban</td>
      <td>31</td>
      <td>26.990323</td>
      <td>26.990323</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Lisatown</td>
      <td>47</td>
      <td>Urban</td>
      <td>23</td>
      <td>22.225217</td>
      <td>22.225217</td>
    </tr>
    <tr>
      <th>27</th>
      <td>New Aaron</td>
      <td>60</td>
      <td>Urban</td>
      <td>22</td>
      <td>26.861818</td>
      <td>26.861818</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Swansonbury</td>
      <td>64</td>
      <td>Urban</td>
      <td>34</td>
      <td>27.464706</td>
      <td>27.464706</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Fosterside</td>
      <td>69</td>
      <td>Urban</td>
      <td>24</td>
      <td>23.034583</td>
      <td>23.034583</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Conwaymouth</td>
      <td>18</td>
      <td>Suburban</td>
      <td>11</td>
      <td>34.591818</td>
      <td>34.591818</td>
    </tr>
    <tr>
      <th>97</th>
      <td>New Lynn</td>
      <td>20</td>
      <td>Suburban</td>
      <td>13</td>
      <td>28.454615</td>
      <td>28.454615</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Port Jose</td>
      <td>11</td>
      <td>Suburban</td>
      <td>18</td>
      <td>31.193889</td>
      <td>31.193889</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Johnland</td>
      <td>13</td>
      <td>Suburban</td>
      <td>18</td>
      <td>28.752778</td>
      <td>28.752778</td>
    </tr>
    <tr>
      <th>100</th>
      <td>West Tony</td>
      <td>17</td>
      <td>Suburban</td>
      <td>19</td>
      <td>29.609474</td>
      <td>29.609474</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Campbellport</td>
      <td>26</td>
      <td>Suburban</td>
      <td>15</td>
      <td>33.711333</td>
      <td>33.711333</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Port Guytown</td>
      <td>26</td>
      <td>Suburban</td>
      <td>15</td>
      <td>28.242000</td>
      <td>28.242000</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Webstertown</td>
      <td>26</td>
      <td>Suburban</td>
      <td>16</td>
      <td>29.721250</td>
      <td>29.721250</td>
    </tr>
    <tr>
      <th>104</th>
      <td>Clarkstad</td>
      <td>21</td>
      <td>Suburban</td>
      <td>12</td>
      <td>31.051667</td>
      <td>31.051667</td>
    </tr>
    <tr>
      <th>105</th>
      <td>North Tracyfort</td>
      <td>18</td>
      <td>Suburban</td>
      <td>10</td>
      <td>26.856000</td>
      <td>26.856000</td>
    </tr>
    <tr>
      <th>106</th>
      <td>Martinmouth</td>
      <td>5</td>
      <td>Suburban</td>
      <td>9</td>
      <td>30.498889</td>
      <td>30.498889</td>
    </tr>
    <tr>
      <th>107</th>
      <td>New Jessicamouth</td>
      <td>22</td>
      <td>Suburban</td>
      <td>17</td>
      <td>32.810588</td>
      <td>32.810588</td>
    </tr>
    <tr>
      <th>108</th>
      <td>South Elizabethmouth</td>
      <td>3</td>
      <td>Rural</td>
      <td>5</td>
      <td>28.698000</td>
      <td>28.698000</td>
    </tr>
    <tr>
      <th>109</th>
      <td>East Troybury</td>
      <td>3</td>
      <td>Rural</td>
      <td>7</td>
      <td>33.244286</td>
      <td>33.244286</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Kinghaven</td>
      <td>3</td>
      <td>Rural</td>
      <td>6</td>
      <td>34.980000</td>
      <td>34.980000</td>
    </tr>
    <tr>
      <th>111</th>
      <td>New Johnbury</td>
      <td>6</td>
      <td>Rural</td>
      <td>4</td>
      <td>35.042500</td>
      <td>35.042500</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Erikport</td>
      <td>3</td>
      <td>Rural</td>
      <td>8</td>
      <td>30.043750</td>
      <td>30.043750</td>
    </tr>
    <tr>
      <th>113</th>
      <td>Jacksonfort</td>
      <td>6</td>
      <td>Rural</td>
      <td>6</td>
      <td>32.006667</td>
      <td>32.006667</td>
    </tr>
    <tr>
      <th>114</th>
      <td>Shelbyhaven</td>
      <td>9</td>
      <td>Rural</td>
      <td>6</td>
      <td>34.828333</td>
      <td>34.828333</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Matthewside</td>
      <td>4</td>
      <td>Rural</td>
      <td>4</td>
      <td>43.532500</td>
      <td>43.532500</td>
    </tr>
    <tr>
      <th>116</th>
      <td>Kennethburgh</td>
      <td>3</td>
      <td>Rural</td>
      <td>10</td>
      <td>36.928000</td>
      <td>36.928000</td>
    </tr>
    <tr>
      <th>117</th>
      <td>South Joseph</td>
      <td>3</td>
      <td>Rural</td>
      <td>12</td>
      <td>38.983333</td>
      <td>38.983333</td>
    </tr>
    <tr>
      <th>118</th>
      <td>Manuelchester</td>
      <td>7</td>
      <td>Rural</td>
      <td>1</td>
      <td>49.620000</td>
      <td>49.620000</td>
    </tr>
    <tr>
      <th>119</th>
      <td>Stevensport</td>
      <td>6</td>
      <td>Rural</td>
      <td>5</td>
      <td>31.948000</td>
      <td>31.948000</td>
    </tr>
    <tr>
      <th>120</th>
      <td>North Whitney</td>
      <td>10</td>
      <td>Rural</td>
      <td>10</td>
      <td>38.146000</td>
      <td>38.146000</td>
    </tr>
    <tr>
      <th>121</th>
      <td>East Stephen</td>
      <td>6</td>
      <td>Rural</td>
      <td>10</td>
      <td>39.053000</td>
      <td>39.053000</td>
    </tr>
    <tr>
      <th>122</th>
      <td>East Leslie</td>
      <td>9</td>
      <td>Rural</td>
      <td>11</td>
      <td>33.660909</td>
      <td>33.660909</td>
    </tr>
    <tr>
      <th>123</th>
      <td>Hernandezshire</td>
      <td>10</td>
      <td>Rural</td>
      <td>9</td>
      <td>32.002222</td>
      <td>32.002222</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Horneland</td>
      <td>8</td>
      <td>Rural</td>
      <td>4</td>
      <td>21.482500</td>
      <td>21.482500</td>
    </tr>
    <tr>
      <th>125</th>
      <td>West Kevintown</td>
      <td>5</td>
      <td>Rural</td>
      <td>7</td>
      <td>21.528571</td>
      <td>21.528571</td>
    </tr>
  </tbody>
</table>
<p>126 rows × 6 columns</p>
</div>




```python
#Get the required columns for the Scatter Plot
final_df_scatter = final_df[["no. of rides","Average Fare","type","driver_count"]]
final_df_scatter["cmap"] = ""
#Create a dictionary of colors by Type
colors = {"Urban": "Gold", "Suburban": "lightskyblue", "Rural": "lightcoral"}
#Append the Color Mapping to the dataframe based on type  
for index, row in final_df_scatter.iterrows():
    final_df_scatter.set_value(index, "cmap", colors[str(row["type"])])
cmap = final_df_scatter["cmap"]

final_df_scatter
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>no. of rides</th>
      <th>Average Fare</th>
      <th>type</th>
      <th>driver_count</th>
      <th>cmap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>28</td>
      <td>21.806429</td>
      <td>Urban</td>
      <td>63</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>1</th>
      <td>26</td>
      <td>25.899615</td>
      <td>Urban</td>
      <td>8</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>2</th>
      <td>22</td>
      <td>26.169091</td>
      <td>Urban</td>
      <td>12</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>3</th>
      <td>29</td>
      <td>22.330345</td>
      <td>Urban</td>
      <td>34</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>21.332609</td>
      <td>Urban</td>
      <td>52</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>5</th>
      <td>24</td>
      <td>26.823750</td>
      <td>Urban</td>
      <td>4</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>6</th>
      <td>18</td>
      <td>22.368333</td>
      <td>Urban</td>
      <td>70</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>7</th>
      <td>23</td>
      <td>27.220870</td>
      <td>Urban</td>
      <td>37</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>8</th>
      <td>26</td>
      <td>24.207308</td>
      <td>Urban</td>
      <td>70</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>9</th>
      <td>28</td>
      <td>28.428929</td>
      <td>Urban</td>
      <td>66</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21</td>
      <td>29.520476</td>
      <td>Urban</td>
      <td>34</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>11</th>
      <td>27</td>
      <td>22.788889</td>
      <td>Urban</td>
      <td>67</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>12</th>
      <td>29</td>
      <td>25.395517</td>
      <td>Urban</td>
      <td>55</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>13</th>
      <td>22</td>
      <td>26.367727</td>
      <td>Urban</td>
      <td>28</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>14</th>
      <td>25</td>
      <td>27.334800</td>
      <td>Urban</td>
      <td>15</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>15</th>
      <td>32</td>
      <td>27.087500</td>
      <td>Urban</td>
      <td>12</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>16</th>
      <td>31</td>
      <td>24.875484</td>
      <td>Urban</td>
      <td>61</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>17</th>
      <td>27</td>
      <td>22.947037</td>
      <td>Urban</td>
      <td>13</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>18</th>
      <td>26</td>
      <td>20.609615</td>
      <td>Urban</td>
      <td>67</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>19</th>
      <td>27</td>
      <td>23.490000</td>
      <td>Urban</td>
      <td>46</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>27.205500</td>
      <td>Urban</td>
      <td>7</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>21</th>
      <td>27</td>
      <td>26.876667</td>
      <td>Urban</td>
      <td>11</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>22</th>
      <td>28</td>
      <td>24.966786</td>
      <td>Urban</td>
      <td>42</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>23</th>
      <td>28</td>
      <td>27.084286</td>
      <td>Urban</td>
      <td>31</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>24</th>
      <td>31</td>
      <td>25.106452</td>
      <td>Urban</td>
      <td>41</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>25</th>
      <td>31</td>
      <td>26.990323</td>
      <td>Urban</td>
      <td>70</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>26</th>
      <td>23</td>
      <td>22.225217</td>
      <td>Urban</td>
      <td>47</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>27</th>
      <td>22</td>
      <td>26.861818</td>
      <td>Urban</td>
      <td>60</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>28</th>
      <td>34</td>
      <td>27.464706</td>
      <td>Urban</td>
      <td>64</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>29</th>
      <td>24</td>
      <td>23.034583</td>
      <td>Urban</td>
      <td>69</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>96</th>
      <td>11</td>
      <td>34.591818</td>
      <td>Suburban</td>
      <td>18</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>97</th>
      <td>13</td>
      <td>28.454615</td>
      <td>Suburban</td>
      <td>20</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>98</th>
      <td>18</td>
      <td>31.193889</td>
      <td>Suburban</td>
      <td>11</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>99</th>
      <td>18</td>
      <td>28.752778</td>
      <td>Suburban</td>
      <td>13</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>100</th>
      <td>19</td>
      <td>29.609474</td>
      <td>Suburban</td>
      <td>17</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>101</th>
      <td>15</td>
      <td>33.711333</td>
      <td>Suburban</td>
      <td>26</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>102</th>
      <td>15</td>
      <td>28.242000</td>
      <td>Suburban</td>
      <td>26</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>103</th>
      <td>16</td>
      <td>29.721250</td>
      <td>Suburban</td>
      <td>26</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>104</th>
      <td>12</td>
      <td>31.051667</td>
      <td>Suburban</td>
      <td>21</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>105</th>
      <td>10</td>
      <td>26.856000</td>
      <td>Suburban</td>
      <td>18</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>106</th>
      <td>9</td>
      <td>30.498889</td>
      <td>Suburban</td>
      <td>5</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>107</th>
      <td>17</td>
      <td>32.810588</td>
      <td>Suburban</td>
      <td>22</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>108</th>
      <td>5</td>
      <td>28.698000</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>109</th>
      <td>7</td>
      <td>33.244286</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>110</th>
      <td>6</td>
      <td>34.980000</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>111</th>
      <td>4</td>
      <td>35.042500</td>
      <td>Rural</td>
      <td>6</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>112</th>
      <td>8</td>
      <td>30.043750</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>113</th>
      <td>6</td>
      <td>32.006667</td>
      <td>Rural</td>
      <td>6</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>114</th>
      <td>6</td>
      <td>34.828333</td>
      <td>Rural</td>
      <td>9</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>115</th>
      <td>4</td>
      <td>43.532500</td>
      <td>Rural</td>
      <td>4</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>116</th>
      <td>10</td>
      <td>36.928000</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>117</th>
      <td>12</td>
      <td>38.983333</td>
      <td>Rural</td>
      <td>3</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>118</th>
      <td>1</td>
      <td>49.620000</td>
      <td>Rural</td>
      <td>7</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>119</th>
      <td>5</td>
      <td>31.948000</td>
      <td>Rural</td>
      <td>6</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>120</th>
      <td>10</td>
      <td>38.146000</td>
      <td>Rural</td>
      <td>10</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>121</th>
      <td>10</td>
      <td>39.053000</td>
      <td>Rural</td>
      <td>6</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>122</th>
      <td>11</td>
      <td>33.660909</td>
      <td>Rural</td>
      <td>9</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>123</th>
      <td>9</td>
      <td>32.002222</td>
      <td>Rural</td>
      <td>10</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>124</th>
      <td>4</td>
      <td>21.482500</td>
      <td>Rural</td>
      <td>8</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>125</th>
      <td>7</td>
      <td>21.528571</td>
      <td>Rural</td>
      <td>5</td>
      <td>lightcoral</td>
    </tr>
  </tbody>
</table>
<p>126 rows × 5 columns</p>
</div>




```python
#Set the properties for the Scatter Plot
plt.xlim(0, max(x)+5)
plt.ylim(0, max(y)+5)
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.title("Pyber Ride Sharing Data (2016)")
```




    Text(0.5,1,'Pyber Ride Sharing Data (2016)')




```python
# Plot the Bubble Chart
plt.scatter(x, y, s=s*8, c=final_df_scatter["cmap"],edgecolors="black",alpha=0.75)

plt.show()
```


![png](output_11_0.png)



```python
#Total % of Fares by Type
#Merge the city data and driver data
#ridecitymerge_city = ride_data_df.merge(city_data_df,on="city")
#Get total fare
totalfare = ridecitymerge_city["fare"].sum()
#Get unique types
types = ridecitymerge_city["type"].unique()
#Group the merged data by type
faresbytype = ridecitymerge_city.groupby(["type"])
#Get total % of fares by type from groped data
totalfaresbytype = faresbytype["fare"].sum()/totalfare * 100
#Create a Data Frame for total % of fare by type
totalfaresbytypedf=pd.DataFrame(totalfaresbytype)
totalfaresbytypedf
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fare</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>6.579786</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>31.445750</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>61.974463</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total % of Fares by Type - Pie Chart
# Labels for the sections of our pie chart
labels = totalfaresbytypedf.index
labels
# The values of each section of the pie chart
sizes = totalfaresbytypedf["fare"] 

# The colors of each section of the pie chart
colors = ["lightcoral","lightskyblue","gold"]

# Tells matplotlib to seperate the "Python" section from the others
explode = (0, 0, 0.1)

```


```python
#Creating Pie Chart
plt.pie(sizes, explode=explode, labels=labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)
```




    ([<matplotlib.patches.Wedge at 0x25cd8ca4160>,
      <matplotlib.patches.Wedge at 0x25cd8ca4ba8>,
      <matplotlib.patches.Wedge at 0x25cd8cac668>],
     [Text(-0.969829,0.519068,'Rural'),
      Text(-0.839065,-0.711316,'Suburban'),
      Text(1.05512,0.571596,'Urban')],
     [Text(-0.528998,0.283128,'6.6%'),
      Text(-0.457672,-0.387991,'31.4%'),
      Text(0.615487,0.333431,'62.0%')])




```python
plt.axis("equal")
plt.title("% of Total Fares by City Type")
```




    Text(0.5,1,'% of Total Fares by City Type')




```python
# Prints our pie chart to the screen
plt.show()
```


![png](output_16_0.png)



```python
#Total % of Riders by Type
#Get total riders
totalriders = ridecitymerge_city["ride_id"].sum()
#Get unique types
types = ridecitymerge_city["type"].unique()
#Group total riders by type
ridersbytype = ridecitymerge_city.groupby(["type"])
#Get Total % of Riders by Type
totalridersbytype = ridersbytype["ride_id"].sum()/totalriders * 100
# Create a Data Frame with Total % of Riders by Type
totalridersbytypedf=pd.DataFrame(totalridersbytype)
totalridersbytypedf
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ride_id</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>5.635701</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>26.860433</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>67.503865</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total % of Riders by Type - Pie Chart
# Labels for the sections of our pie chart
labels1 = totalridersbytypedf.index

# The values of each section of the pie chart
sizes1 = totalridersbytypedf["ride_id"] 

# The colors of each section of the pie chart
colors1 = ["lightcoral","lightskyblue","gold"]

# Tells matplotlib to seperate the "Python" section from the others
explode1 = (0, 0, 0.1)
labels1
```




    Index(['Rural', 'Suburban', 'Urban'], dtype='object', name='type')




```python
plt.pie(sizes1, explode=explode1, labels=labels1, colors=colors1,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.axis("equal")
plt.title("Total % of Riders by Type")
plt.show()
```


![png](output_19_0.png)



```python
#Total % of Drivers by Type
#Get Total Drivers
totaldrivers = ridecitymerge_city["driver_count"].sum()
#Get Unique Types
types = ridecitymerge_city["type"].unique()
#Group drivers by type
driversbytype = ridecitymerge_city.groupby(["type"])
#Get Total % of Drivers by Type
totaldriversbytype = driversbytype["driver_count"].sum()/totaldrivers * 100
#Create a data frame for Total % of Drivers by Type
totaldriversbytypedf=pd.DataFrame(totaldriversbytype)
totaldriversbytypedf
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>type</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rural</th>
      <td>0.969876</td>
    </tr>
    <tr>
      <th>Suburban</th>
      <td>12.980602</td>
    </tr>
    <tr>
      <th>Urban</th>
      <td>86.049521</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Total % of Drivers by Type - Pie Chart
# Labels for the sections of our pie chart
labels2 = totaldriversbytypedf.index
labels2
# The values of each section of the pie chart
sizes2 = totaldriversbytypedf["driver_count"] 

# The colors of each section of the pie chart
colors2 = ["lightcoral","lightskyblue","gold"]

# Tells matplotlib to seperate the "Python" section from the others
explode2 = (0, 0, 0.1)
```


```python
#Pie Char for Total % of Drivers by Type
plt.pie(sizes2, explode=explode2, labels=labels2, colors=colors2,
        autopct="%1.1f%%", shadow=True, startangle=140)
plt.axis("equal")
plt.title("Total % of Drivers Fares by Type")
plt.show()
```


![png](output_22_0.png)


# Chapel Hill Demo Map
```
import pandas as pd
import requests
import numpy as np
import folium
import folium.plugins
from folium.plugins import MarkerCluster
```
```
def folium_deepnote_show(m):
    data = m.get_root().render()
    data_fixed_height = data.replace('width: 100%;height: 100%', 'width: 100%').replace('height: 100.0%;', 'height: 609px;', 1)
    display(HTML(data_fixed_height))
```

```
chapel_hill=pd.read_csv('/Users/sunhuiqing/Desktop/ChapelHillEVData.csv', delimiter=',')
```
·If you want to run these codes, please use this [ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv) to replace my local read csv file.


```
def categorycolors(chapel_hill):
    if chapel_hill['Category'] == 'Smells':
        return 'green'
        
    elif chapel_hill['Category'] == 'WTP':
        return 'blue'
        
    elif chapel_hill['Category']== 'Superfund':
        return 'red'
        
    elif chapel_hill['Category'] == 'Vultures':
        return 'purple'
        
    elif chapel_hill['Category']== 'Park':
        return 'yellow'
        
    else:
        return 'darkblue'
 ```      
        
·chapel_hill["color"] = chapel_hill.apply(categorycolors, axis=1)
[ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv) contains names and categories of addresses, as well as the coordinates, and the above codes set different colors to represent different categories: # greens are Smells#, #blues are WTPs, reds are Superfunds, purples are Vultures, yellows are Parks.


```
locations = chapel_hill[['Latititude', 'Longitutude']]\
locationlist = locations.values.tolist()\
```


·The following codes creat an interactive map which contains important addresses (from [ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv)) around chapelhill park.

```
Chapel_Hill_Map = folium.Map(location=[33.6733, -84.2253], tiles='CartoDB positron', zoom_start=11)

marker_cluster = folium.plugins.MarkerCluster().add_to(Chapel_Hill_Map)

for point in range(0, len(locationlist)):
    folium.Marker(locationlist[point], popup='ID:'+str(chapel_hill['id'][point]), icon=folium.Icon(color=chapel_hill["color"][point], icon_color='white', icon='biohazard', angle=0, prefix='fa')).add_to(marker_cluster)
    
Chapel_Hill_Map

```


·Then we think sewer sites of the [priority fix information](https://www.ajc.com/neighborhoods/dekalb/map-the-dekalb-sewer-systems-103-priority-fixes/JBAEM2ABZRAJ3IKQREFKM737S4/)would be helpful, so from this website, we filtered out a few sites near chapel hill park (within twenty or thirty minutes by car), and put thoes sites' name as well as their coordinates into a file which is the [sewer.csv](https://github.com/HuiqingSun/EJProject/blob/main/sewer.csv), and set black as the sewer sites color on the map, then repeat similar code steps above, we added sewer sites to the previous base map.

·sewer status information in this [sewer.csv](https://github.com/HuiqingSun/EJProject/blob/main/sewer.csv) are from [Page19-25]
(https://www.dekalbcountyga.gov/sites/default/files/users/user3551/DeKalb%20County%20Annual%20Report%20No%2010%203.1.22.pdf)


```
sewer=pd.read_csv('/Users/sunhuiqing/Desktop/sewer.csv', delimiter=',')

locations = sewer[['latitude', 'longitude']]
locatel = locations.values.tolist()
def cate(sewer):
    if sewer['cate'] == 'sewersites':
        return 'black'
    else:
        return 'darkblue'
sewer["color"] = sewer.apply(cate, axis=1)
```

```
for point in range(0, len(locatel)):
    folium.Marker(locatel[point], popup='sites:'+str(sewer['sites'][point]), icon=folium.Icon(color=sewer["color"][point], icon_color='white', icon='biohazard', angle=0, prefix='fa')).add_to(marker_cluster)
    
Chapel_Hill_Map

```

·To see the folium map results, please click this [link](http://nbviewer.org/github/HuiqingSun/map/blob/main/Chapel%20Hill%20Demo%20Map%20%284%29%20%282%29.ipynb).

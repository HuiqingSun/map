# Chapel Hill Demo Map

import pandas as pd\
import requests\
import numpy as np\
import folium\
import folium.plugins\
from folium.plugins import MarkerCluster

def folium_deepnote_show(m):\
    data = m.get_root().render()\
    data_fixed_height = data.replace('width: 100%;height: 100%', 'width: 100%').replace('height: 100.0%;', 'height: 609px;', 1)\
    display(HTML(data_fixed_height))


chapel_hill=pd.read_csv('/Users/sunhuiqing/Desktop/ChapelHillEVData.csv', delimiter=',')


def categorycolors(chapel_hill):\
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
       
        
chapel_hill["color"] = chapel_hill.apply(categorycolors, axis=1)
[ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv) contains names and categories of addresses, as well as the coordinates, and the above codes set different colors to represent different categories: greens are Smells, blues are WTPs, reds are Superfunds, purples are Vultures, yellows are Parks.



locations = chapel_hill[['Latititude', 'Longitutude']]\
locationlist = locations.values.tolist()\



The following codes creat an interactive map which contains important addresses (from [ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv)) around chapelhill park.

Then we think sewer sites of the [priority fix information](https://www.ajc.com/neighborhoods/dekalb/map-the-dekalb-sewer-systems-103-priority-fixes/JBAEM2ABZRAJ3IKQREFKM737S4/)would be helpful, so from this website, we filtered out a few sites near chapel hill park (within twenty or thirty minutes by car), and put thoes sites' name as well as their coordinates into a file which is the [sewer.csv](https://github.com/HuiqingSun/EJProject/blob/main/sewer.csv), and set black as the sewer sites color on the map, then repeat similar code steps above, we added sewer sites to the previous base map.

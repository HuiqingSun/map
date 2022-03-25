# map
[ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv) contains names and categories of addresses, as well as the coordinates, and the above codes set different colors to represent different categories: greens are Smells, blues are WTPs, reds are Superfunds, purples are Vultures, yellows are Parks.

The following codes creat an interactive map which contains important addresses (from [ChapelHillEVData.csv file](https://github.com/HuiqingSun/EJProject/blob/main/ChapelHillEVData.csv)) around chapelhill park.

Then we think sewer sites of the [priority fix information]("https://www.ajc.com/neighborhoods/dekalb/map-the-dekalb-sewer-systems-103-priority-fixes/JBAEM2ABZRAJ3IKQREFKM737S4/") would be helpful, so from this website, we filtered out a few sites near chapel hill park (within twenty or thirty minutes by car), and put thoes sites' name as well as their coordinates into a file which is the [sewer.csv](https://github.com/HuiqingSun/EJProject/blob/main/sewer.csv), and set black as the sewer sites color on the map, then repeat similar code steps above, we added sewer sites to the previous base map.

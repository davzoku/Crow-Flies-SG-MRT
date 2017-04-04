# Crow-Flies-SG-MRT
Calculating “As-the-crow-flies” distance between consecutive MRT/LRT stations in Singapore

## Introduction ##

The main purpose of this project is for me to practise data analysis and familiarise with the steps (and javascript) involved. While the information of the aerial distances between the stations may not be as useful as the actual distance (on the road) or the time required for travelling, these aspects can be explored in the future.

Interestingly, similar projects have been explored for the London Underground as means of preparation for the tube challenge. The link is available [here].

## The Thought Process ##

**Step 1:** An efficient way to gather all the Lat, Long coordinates of the train stations

The most efficient method of data gathering is to find the dataset readily available without the need to manually plot all the stations on Google’s My Maps or other GIS program.

Surely, this data set is available on the [Data Mall published by LTA].

There are plenty of geospatial data available on the data mall, presented in .shp format.
Other datasets includes the locations of bus stops, ERP gantry, traffic lights, taxi stand and so on. These datasets may be useful in future projects of similar goals.

However, there are several issues before the information can be used efficiently
* All train stations from all MRT/LRT lines are compressed into a single .shp file. The file would have to be separated into individual train lines before analysis.
* There are repeated entries for interchange stations and their actual points plotted differs from the one displayed on Google Maps. This is logical as LTA provides the actual location underground while Google Maps only shows the station location above ground. For simplification, Google Maps location should be used. (Refer to Fig 1.)
* Newly planned stations that are not yet available are included in the dataset. While it is useful, these cases should be explored later on as the project matures.


![atcf1](https://cloud.githubusercontent.com/assets/16046667/24665508/2d450172-1990-11e7-9053-aed0fc379f62.JPG)

*Fig 1: Repeated entries for interchange stations and the data shows actual physical location underground which complicates the analysis.*


Therefore, plotting the locations manually would have saved a lot of trouble. 

**Step 2:** Spherical Law of Cosine Formula vs Haversine Formula

There are generally 2 variations of formula used for calculation of aerial distance between any 2 coordinates. Read more: [Spherical Law of Cosine Formula], [Haversine Formula]
While the formulas yield very similar results (up to 4 dp in km), there is a discussion on the computation speed. 

![atcf2](https://cloud.githubusercontent.com/assets/16046667/24665509/2d4ad0b6-1990-11e7-9853-8f9a2b6ffd73.JPG)

*Fig 2. [Spherical Law of Cosines vs Haversine]*

For the sake of learning, both formulas were used.

Spherical Formula on excel:
```
=ACOS(SIN(RADIANS(LAT1))*SIN(RADIANS(LAT2))+COS(RADIANS(LAT1))*COS(RADIANS(LAT2))*COS(RADIANS(LON2-LON1)))*6371
```

Haversine Formula on excel:
```
=6371*2*ATAN2(SQRT(1-(SIN(RADIANS((LAT2-LAT1)/2))^2+COS(RADIANS(LAT1))*COS(RADIANS(LAT2))*SIN(RADIANS((LON2-LON1)/2))^2)),SQRT(SIN(RADIANS((LAT2-LAT1)/2))^2+COS(RADIANS(LAT1))*COS(RADIANS(LAT2))*SIN(RADIANS((LON2-LON1)/2)^2)))
```

*To be completed.*

## References: ##

[here]:http://www.thetubechallenge.com/projectplan/primarydatagathering/network-map


[Data Mall published by LTA]:https://www.mytransport.sg/content/mytransport/home/dataMall.html


[Spherical Law of Cosine Formula]:https://en.wikipedia.org/wiki/Spherical_law_of_cosines


[Haversine Formula]:https://en.wikipedia.org/wiki/Haversine_formula


[Spherical Law of Cosines vs Haversine]:http://gis.stackexchange.com/questions/4906/why-is-law-of-cosines-more-preferable-than-haversine-when-calculating-distance-b

http://www.thetubechallenge.com/projectplan/primarydatagathering/network-map


https://www.mytransport.sg/content/mytransport/home/dataMall.html


https://en.wikipedia.org/wiki/Spherical_law_of_cosines


https://en.wikipedia.org/wiki/Haversine_formula


http://gis.stackexchange.com/questions/4906/why-is-law-of-cosines-more-preferable-than-haversine-when-calculating-distance-b


https://webtrough.wordpress.com/2011/09/19/latlon-distance-formula-in-excel-haversine-and-spherical-law-of-cosines/


http://bluemm.blogspot.sg/2007/01/excel-formula-to-calculate-distance.html


http://www.movable-type.co.uk/scripts/latlong.html



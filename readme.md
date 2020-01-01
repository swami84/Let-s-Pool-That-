# NYC Taxi Ride Clustering to Enhance Carpool Efficiency

Due to high population density in NY, there is a high demand for ride hailing services such as Uber, Lyft, Yellow Cab, VIA etc. However, majority (>75%) of the yellow cab rides are single passenger trips.

![Image 1](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Passenger%20Count%20per%20Trip%20Distribution.jpg)

Passenger Per Trip|Trip Count|Percentage of Trips
---|---|---
1|1570057|77.74
2|315689|15.63
3|91425|4.53
4|42524|2.11


While being exclusive, single passenger trips lead to higher cost, carbon emission and traffic congestion. The aim of this project is to look at machine learning techniques to aggregate yellow cab rides to pool passengers and optimize these techniques to enhance single trip to pool trip conversion efficiency


#### Aggregating  these trips such that at a given time passengers carpool from similar pickup and dropoff locations can lead to 

> - ***Lower Carbon emission***
> - ***Cost ($) savings for passengers***
> - ***Lower road traffic congestion***
> - ***Demand predicition that can enable efficient fleet management and scheduling***



For best results please see [NBViewer](https://nbviewer.jupyter.org/github/swami84/Let-s-Pool-That-/blob/master/NYC_Carpool_Clustering%20Analysis.ipynb?flush_cache=true) to see the jupyter notebook. 


Data sources:

• NYC taxi data [TLC](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
 
• NYC borough [polygons](https://data.cityofnewyork.us/City-Government/Borough-Boundaries/tqmj-j8zm)

Yellow cab trip data in Manhattan region has been analyzed. One week of the trip data is utlized and two different ways of clustering using different features is employed. Their efficiency in passenger and trip reduction  is compared at different time of the day. Further, prime locations for high efficiency carpooling are identified and visualized

### Why Manhattan??

* High demand area
* Passengers are less likely to have luggage/larger items
* Well ...its MANHATTAN!!!

#### Approach

* Aggregate rides based on pick-up and drop-off information using clustering 

#### Efficiency

* Defined by total reduction in trips as well as reduction of single passenger trips

#### Assumptions

* Drivers/Cars is available at all spatial locations under consideration
* Riders are comfortable walking ~ 0.1  mile (2-3 blocks) for pick-up and from drop-off locations
* Max of 4 passengers per car 

#### Clustering Model

* Algorithm: K-Means
* Data grouped by time (freq =5 min) and Weekday
* Clusters chosen to keep centroids close  (0.1 mile) to pickups and drop-offs. Correlated inertia (distortion) to pickup distance and used Random Forest regression to choose number of clusters

#### Efficiency Definition

![Image 2](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Efficiency%20Equations.PNG)


## Cluster - Size - Pickup Distance Correlation

- Pickup distance varies with size of the dataset and inertia (mean distance between the cluster centroid and pickup location). Relationship is non-linear
- Used a random forest regression model to predict inertia and used it to estimate cluster size

<p align="center">
  <img src="https://github.com/swami84/NYC-Yellow-Cab-Clustering-for-Carpool/blob/master/Images/3D%20Surface%20plot_Size_Distance_Distortion_fit.jpg" />
</p>


## Method 1: Clustering Pickup and Dropoff Locations

- Aggregating rides based on clustering pickup and drop-off locations
- Features clustered – Pickup (latitude, longitude) and Drop-off (latitude, longitude) 

![Image 3](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Method%201_Pickups%20and%20Dropoff.png)


## Method 2: Clustering Pickup Location and Dropoff Angle and Distance

- Clustering rides based on pick-up location and drop-off bearing angle and distance
- Lower weightage given to bearing angle and distance to ensure proximity of centroid to requested pickups

<p align="center">
  <img src="https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Method%202_Pickups%20and%20Dropoff.png" />
</p>



## Results: Efficiency vs Method

![Image 5](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Single%20Ride%20Conversion%20Efficiency_Hour.jpg)

![Image 6](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Overall%20Ride%20Conversion%20Efficiency_Hour.jpg)


- Method 2 performs better than Method 1 in overall and single ride conversion
- Both methods significantly reduce single passenger trips 
- Low conversion efficiency at early hours (2- 4 AM) due to lower number of rides and higher dispersion


## Neighborhood Comparison

- Neighborhoods and locations near central park and lower Manhattan are spots of high efficiency
- Method 2 performs slightly better in the southern neighborhoods


![Image 7](https://github.com/swami84/Let-s-Pool-That-/blob/master/Images/Neighbohood%20Passenger%20Efficiency.png)

<p></p>

# Insights

* Clustering analysis helps in active fleet management and scheduling which can lower customer waiting time 
* Insights from spatio temporal trends allows rideshare networks to predict demand, allocate resources and minimize delays
* Further, the two methods proposed can serve as cost effective pooling services 
    - Where Method 2 can be provided as the lower cost among the two 


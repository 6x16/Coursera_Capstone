# Final Capstone Project - Project Report
## Descriptive title: New York's Borough Investigation
## Preface
_Now, after acquiring the skills and the tools to use location data to explore a geographical location, this is a final project to illustrate an idea to leverage the Foursquare location data to explore or compare neighborhoods or cities, or to come up with a problem that can use the Foursquare location data to solve._
************************************
## Table of Contents

1. <a href="#1-introduction-and-business-problem">Introduction and Business Problem</a>
2. <a href="#2-data-and-materials">Data and Materials</a>  
3. <a href="#3-methodology">Methodology</a>
4. <a href="#4-results">Results </a>  
5. <a href="#5-discussion">Discussion</a>  
6. <a href="#6-conclusion">Conclusion</a>  
***********************************
## 1. Introduction and Business Problem
Although we have the information of neighbourhoods in Manhattan, for **the urban planners and government who are my audience**, they may want to know more about how other boroughs are like and how the KMeans-clustered neighbourhoods are actually close to each other, which will relate to their ability to coorporate with each other for boosting tourisms and the ease of future planning.

Here, we will continue the work of clustering and segmentation of New York mentioned in our course, but we will investigate the other boroughs as well. Once we obtain thier geographical data, we will conduct K-Means clustering neighbourhoods-wise and DBSCAN, which is a common spatial clustering method, on each resulting cluster. For only prove-of-concept, we will choose **The Bronx** as our another target borough since it has similar estimated population with **Manhattan** (Reference: [Wikipedia](https://en.wikipedia.org/wiki/Boroughs_of_New_York_City)).
Hence, we have two questions here:
1. Illustrate how the clusters of Manhattan and The Bronx are different/similar after K-Mean clustering.
2. Using spatial clustering, find out whether the neighbourhoods belonged to the same clusters above are really close to each other.

## 2. Data and Materials
Here, we will use two different sets of data: one is New York neighborhood data with 5 boroughs and 306 neighborhoods, published by [NYU Spatial Data Repository](https://geo.nyu.edu/catalog/nyu_2451_34572); the another one is FourSquare data for exploring the neighbourhoods of the two targeted boroughs (Foursquare API will be used, details will be presented in _Methodology_). 

**A. New York neighborhood spatial data (partial, only for demostration):**

index | Borough | Neighborhood | Latitude | Longitude
--- | --- | --- | --- | ---  
0 |	Bronx |	Wakefield	| 40.894705 | -73.847201
1 |	Bronx |	Co-op City | 40.874294 	| -73.829939
2 |	Bronx |	Eastchester | 40.887556 | -73.827806
3 |	Bronx |	Fieldston | 40.895437 | -73.905643
4 |	Bronx |	Riverdale | 40.890834 | -73.912585

**B. FourSquare neighbourhoods data (partial, only for demostration):**

Index |	name | categories | lat | lng
--- | --- | --- | --- | ---
0 | Arturo's | Pizza Place | 40.874412 | -73.910271
1 | Bikram Yoga | Yoga Studio | 40.876844 | -73.906204
2 | Tibbett Diner | Diner | 40.880404 | -73.908937
3 | Starbucks | Coffee Shop | 40.877531 | -73.905582
4 | Dunkin' | Donut Shop | 40.877136 | -73.906666

## 3. Methodology
In this project, we have conducted clustering analyses by **K-mean clustering** and **DBSCAN clustering**. With combining these two machine learning methods, we can see how the similar places/neighborhoods are distributed geologically and the similarity, if any, between Manhattan and The Bronx in terms of their neighborhoods clustering.
The following links may be referred for detailed methodology illustration:

[Dynamic Preview of Jupyter Notebook](https://nbviewer.jupyter.org/github/6x16/Coursera_Capstone/blob/master/NY_Borough_Investigation.ipynb)

[Github notebook](https://github.com/6x16/Coursera_Capstone/blob/master/NY_Borough_Investigation.ipynb)
### 3.1 K-mean clustering
FourSquare API was packaged into a self-defined function (i.e. getNearbyVenues(), please refer to Jupyter Notebook for detailed codes) and it was used to retrieve the venue data from all neighbourhoods in both Manhattan and Bronx. Once the dataframe of venues in each borough was obtained, a built-in functions of _Pandas_, _get_dummies_, was used to convert the categorical table into pivot talbe-like tabular format with relative frequencies (i.e. grouped_clustering). 

K-mean clustering parameter was set as 5 (**i.e. number of clusters = 5**), similar to previous tutorial, and a _scikit-learn_ function, _KMeans(n_clusters=kclusters, random_state=0).fit(grouped_clustering)_, was used. The output for each neighborhood was the corresponding cluster label, which indicated which group should that neighborhood belonged to based on its containing venues compared with other similar neighborhoods.

### 3.2 DBSCAN clustering
Similar to K-mean clustering method, FourSquare data was used in here. Yet, for spatial clustering, the results returned illustrated how the neighborhoods in a borough were close to or far away from each other and how they were grouped by spatial distance. Here, a _scikit-learn.cluster_ function, _DBSCAN(eps, min_samples).fit(data_df)_, was used. The corresponding parameters were **eps=0.5** and **min_samples=3** based on technical trials previously; also, _data_df_ contained the latitude and longitude values of all neighborhoods in either borough. 

The output for each neighborhood was the corresponding cluster label, which indicated which group should that neighborhood belonged to based on the distance between other different neighborhoods and **label 0** was used to identify noises in all both clustering results of Manhattan and Bronx.
## 4. Results
In this project, we were only looking at 2 boroughs, which were Manhattan and Bronx, for clustering comparison. The entire New York city borough map was shown here to reveal the details of geographical location and description of New York city.
<img src='https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/maps/newyork_map.jpg' height=500 width=800>
### 4.1 K-mean clustering
#### Manhattan
Briefly, under K-mean clustering, 5 clusters have been formed for both Manhattan and Bronx, individually. Here are the neighborhoods results for Manhattan:
- [Cluster 1: 17](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_kmean_cluster1.docx)
- [Cluster 2: 11](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_kmean_cluster2.docx)
- [Cluster 3: 1](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_kmean_cluster3.docx)
- [Cluster 4: 1](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_kmean_cluster4.docx)
- [Cluster 5: 10](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_kmean_cluster5.docx)

Below is the map visualization of K-mean clustering for Manhattan:
<img src='https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/maps/manhattan_kmean.jpg' height=500 width=800>

#### The Bronx
Similarly, neighborhoods in Bronx were also been clustered and clusters were formed based on categorical venues frequencies. Here are the neighborhoods results for Bronx: 
- [Cluster 1: 4](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_kmean_cluster1.docx)
- [Cluster 2: 39](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_kmean_cluster2.docx)
- [Cluster 3: 7](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_kmean_cluster3.docx)
- [Cluster 4: 1](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_kmean_cluster4.docx)
- [Cluster 5: 1](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_kmean_cluster5.docx)

Below is the map visualization of K-mean clustering for Bronx:
<img src='https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/maps/bronx_kmean.jpg' height=500 width=700>

### 4.2 DBSCAN clustering
#### Manhattan
For DBSCAN clustering, Manhattan has returned only **2 formal clusters and 3 noise neighborhoods** by defined parameters (in order to refer the full data, please click into the link of each cluster count number to access the respective document):
- [Cluster 1: 32](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_dbscan_cluster1.docx)
- [Cluster 2: 5](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_dbscan_cluster2.docx)
- [Noises: 3](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/manhattan_dbscan_noises.docx)

Below is the map visualization of DBSCAN clustering for Manhattan:
<img src='https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/maps/manhattan_dbscan_label.jpg' height=500 width=500>

#### Bronx
Likewise, Bronx has been performed clustering and returned **3 formal clusters and 5 noise neighborhoods** by defined parameters:
- [Cluster 1: 22](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_dbscan_cluster1.docx)
- [Cluster 2: 22](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_dbscan_cluster2.docx)
- [Cluster 3: 3](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_dbscan_cluster3.docx)
- [Noises: 5](https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/bronx_dbscan_noises.docx)

Below is the map visualization of DBSCAN clustering for Manhattan:
<img src='https://github.com/6x16/Coursera_Capstone/blob/master/Results_finalproject/maps/bronx_dbscan_label.jpg' height=500 width=600>

## 5. Discussion
#### Observations:

#### Recommendations/Suggestions:

## 6. Conclusion

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
#### Manhattan:
Although these two close-with-each-other boroughs are similar in term of population size, they have obvious differences of urban planning and characteristics, which may help us to discover in what direction, for urban developer and govermnet, we can develop them in the future.

By K-mean clustering, Manhattan had three clusters similar in neighborhood numbers, these three clusters were distributed into a seemingly regular way, which is top(orange), bottom-left(red) and bottom-right(purple). The top-10 most common places in the largest cluster (cluster 1, red, 17 neighborhoods) included restaurants which are selling different cuisines but not only one, and recreational facilities (fitness centre and theatre) as the most; while the 2nd-large (cluster 2, purple, 11 neighborhoods) and 3rd-large clusters (cluster 5, 10 neighborhoods, orange) contains mainly restaurants. However, when we look at DBSCAN results, the three neighborhoods, which belong to cluster 5 in K-mean results, were identified as **noise (red in color)**; the neighborhoods at the bottom of Manhattan, which were mainly cluster1 and 2, were grouped together based on spatial features. 

With this comparisonn, we can know that the neighborhoods at the bottom part were not only close to each other, but also share very similar characteristics, people living in there can usually have easy access on foods/alcohols and recreational facilities (park, spa, fitness centre, etc.). The three noise neighborhoods **(Mable Hill, Inwood, Washington Heights)**, though had similar features on other neighborhoods (many restaurants and only few recreational venues), were far away from others, and so, it was expected that access to different venues and facilities were not convenient compared to the neighborhoods at the bottom. Interestingly, the 4th common venue in Washington Heights was **"Mobile phone shop"**, which did not exist in the top 2 largest clusters and it may be because only few shops were selling electronic gadgets in those areas and most people could only go to this venus to buy new electonic devices; conversely, at the bottom, shops were crowded together, and so, people have more choices on buying electronic devices so that "Mobile phone shop" was relatively less common.

#### Bronx:
On the other hand, Bronx had one very large cluster in K-mean clustering results (cluster 1, 39 neighborhoods, purple). Different from the large clusters in Manhattan, this cluster contained diverse categories of venues, including foods/restaurants, recreationals, transportations, banks, pharmacies and different types of goods-selling stores. This revealed that people living there were actually more willing to take transportations to go to different places, so that the mobility in these areas were stronger than in Manhattan. Also, as we could see that diverse types of venues were identified as common venues, we hypothesized that people living there are more likely going to different shops in-person to buy things, while people in Manhattan like to buy things via other approaches, such as e-commerce, as there are much fewer shops were identified as common venues.

While, under DBSCAN clustering, two large clusters similar in size (cluster 2, blue; cluster 1, purple) were formed on left and right side respectively. This might help to show that, people living in these two clusters were less convenience to go across the clusters, so it actually revealed the most possible neighborhoods where the people living in different clusters might go. Notably, **Spuyten Duyvil**, which belonged to cluster 1 (red) in K-mean clustering and cluster 2 (blue) in DBSCAN clustering, is the neighborhood which is closest to Manhattan's neighborhood, **Marble Hill**. These two neighborhoods could not only be intersection places between these two boroughs, but also have potentials to coorporate with each other and develop tourisms.

Neighborhood | 1st Most Common Venue | 2nd Most Common Venue | 3rd Most Common Venue | 4th Most Common Venue | 5th Most Common Venue | 6th Most Common Venue | 7th Most Common Venue | 8th Most Common Venue | 9th Most Common Venue | 10th Most Common Venue
--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- 
Marble Hill | Sandwich Place | Coffee Shop | Yoga Studio | Diner | Steakhouse | Miscellaneous Shop | Supplement Shop | Shopping Mall | Tennis Stadium | Seafood Restaurant
Spuyten Duyvil | Tennis Stadium | Pharmacy | Park | Intersection | Bus Line | Bus Stop | Scenic Lookout | Thai Restaurant | Bank | Tennis Court

#### Recommendations/Suggestions:
However, since this project is only a short project, further investigations can be done in order to provide more information for future development. Firstly, more boroughs can be studied so that we can have a more comprehensive picture of how the whole New York city looks like and it will help us to make further decisions. Secondly, a more detailed statistics can be done on all venues by keyword searching/category classifications, so that we can know more about how frequent and why the most common venues are visited by people.

## 6. Conclusion
In conclusion, K-mean clustering and DBSCAN clustering have been conducted to analyze the neighborhoods in both Manhattan and Bronx. We found that Spuyten Duyvil and Marble Hill are the potential neighborhoods which provide opportunity to urban planners to develop cross-borough tourism based on the fact that their most common venues includes most of the necessary parts of our daily life.

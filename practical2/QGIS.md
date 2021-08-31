# Exercise 2: opening and analyzing the data in QGIS

Now that we have all the data in our folder, we can open QGIS and load the vector (shapefile) of the watersheds, and the two rasterfiles (the biodiversity tif and the NDVI tif files).



https://user-images.githubusercontent.com/89069805/131482487-7562b9c7-afd5-4512-8ad1-7754e3b532fb.mp4




Now we get to the core objective of the exercise: what is the link between biodiversity and available vegetation? 


### To answer this question, we'll need to decide and simplify (course 1, slide 45)
* Geographic scale – spatial unit 
* Temporal scale 
* Boundary conditions/assumptions
* Dimensions (which processes and structures will you account for, which not)
* Dimension descriptions (how do you approximate/describe the dimension)

Of course, for the purpose of this exercise, these decisions have already been taken, and are summarized here: 
| building block  |  decision |
|---|---|
| Geographic scale |  Watersheds |
| temporal scale |  similar timespans need to be covered and aggregated over sufficiently large timespan |
| Assumption | more primary producers = more available energy, resulting into a higher biodiversity |
| Dimensions | We'll consider vegetation cover and mammal biodiversity |
| Dimension description | MODIS NDVI (as proxy for vegetation) and mammal species richness by biodiversity.org |



### Now that we have simplified we can take the average species richness and average NDVI per watershed

* because both are averages over a spatial unit, the size of the spatial unit is not explicitally corrected for here
* we'll use the function *zonal statistics* in the QGIS toolbox to calculate this



https://user-images.githubusercontent.com/89069805/131485589-8a7ddc91-cf03-4f07-a731-8052861a1f7b.mp4



Our vector file now has two extra attribute columns: mean NDVI and mean mammal richness. 

### Can we now visualize this relationship? 

* QGIS (and many others) are typically used for visualization and analysis of geographic (spatial) data
* But, some basic analytic figures can be made as well, e.g. a Scatterplot: 



https://user-images.githubusercontent.com/89069805/131485805-9f4a6e92-9cd7-4e7c-a743-3c327c759505.mp4



# Exercise 2: opening and analyzing the data in QGIS

Now that we have all the data in our folder, we can open QGIS and load the vector (shapefile) of the watersheds, and the two rasterfiles (the biodiversity tif and the NDVI tif files).



https://user-images.githubusercontent.com/89069805/131482487-7562b9c7-afd5-4512-8ad1-7754e3b532fb.mp4




Now we get to the core objective of the exercise: what is the link between biodiversity and available vegetation? 


## To answer this question, we'll need to decide and simplify (course 1, slide 45)
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

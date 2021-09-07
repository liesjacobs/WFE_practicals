# Step 2: Data Retrieval 

The easiest set to download are the administrative boundaries of Belgium, this is through a direct download
[here](https://biogeo.ucdavis.edu/data/diva/adm/BEL_adm.zip)

>Unzip the file: you'll see it countains shapefiles on many administrative levels: only those at the 0th level are of interest to us: 
>>make sure all files coded with BEL_adm0 (so all files starting with these letters, regardless of the file extension) are stored in an appropriate folder (e.g. a folder 'Belgium' in the folder you made for this practical. 


>Now that we have the shapefile, let's open in it in QGIS and subdivide it in smaller spatial units (polygons in the shape of gridcells) that we can use to do our analysis. 
>>Because the shapefile of Belgium is referenced in WGS84 ( so it has geographical coordinates in degrees rather than x,y coordinates in meters) the unit of subdivision is also in degrees. Note that it would be more correct to convert all layers to a projected coordinate system (e.g. UTM). For the purpose of this exercise, we'll keep all data in WGS84.
>>To subdivide the territory, we'll need two functions: *Create Grid* function you'll find under the 'vector' tab, and finally, you'll need to clip the created grid again with the boundary layer of belgium, so that you only keep those grids that fall within the country: 'Vector'-->'Geoprocessing tools'-->'Clip'


<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132325445-4ce14f7e-e7fe-4906-a606-bf905a0db358.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>



***

Now, let's try a 'point and click' plugin that enables an OSM API plugin in QGIS. 

>We'll first need to install this plugin "QuickOSM": this is shown in the video below. 

<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132320601-a94f04d6-503d-4da8-9edd-23f18f8a399e.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


>Great, now we can actually use the plugin to download the rivers of Belgium. Following steps/details are needed:
>>Open the plugin (the green magnifying glass in the upper left corner)
>>Rivers in OSM belong to the *Key* 'Waterway' and the *Value* 'River'. 
>>For the location, we want to use the administrative boundary of belgium we just downloaded
>>Because the data we try to access is quite a large set, we'll increase the time allowed (before an error is trown) to 200 seconds (under advanced settings). We also untick the 'node'box, the 'relation' box, the 'points' box and the 'mulitpolygons' : rivers are coded as 'Ways'in OSM and as lines or multilinestrings, so by unticking the other boxes, we'll remove unnecessary searches. 
>>The Final interface of the plugin should look like this: 


![osmplugin](https://user-images.githubusercontent.com/89069805/132326967-ca2acb13-fdd6-4bb7-8236-6fb4f322879b.png)

>>now you can click on *Run query* and wait


***

Now that we have our river layer, we can download the raster fill for topographic diversity. Luckily, we already know how, as this layer is available in GEE, so we can clip the image we need, and export it to our google drive, and from there, download it: 

```javascript

var belgium_window = 
    ee.Geometry.Polygon(
        [[[0.267, 51.908],
          [0.267, 48.623],
          [8.946, 48.623],
          [8.946, 51.908]]]);

var topo = ee.Image("CSP/ERGo/1_0/Global/ALOS_topoDiversity").clip(belgium_window);
print(topo);

Map.addLayer(topo);

//what is the resolution? 
print(topo.projection().nominalScale());

Export.image.toDrive({
  image: topo,
  description: 'topodivALOS',
  scale: 270,
  fileFormat: 'GeoTIFF'
});



```

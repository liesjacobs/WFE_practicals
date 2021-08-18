### Exercise 3: Understanding the Gradient : how process influences form

In this exercise we will actually *use* data from earth engine to gain insight in a real-life question: 
How can we explain the remarkable gradient in land cover (and related agricultural practices) along the West-Coast of the USA (see slides 32-33 course 1)



> step 1: make a new Script in Earth engine, and give it an appropriate name (e.g. transects)




Now we can think about the building blocks of the analysis (see slide 45, course 1): 
- what Geographic scale – spatial unit is appropriate
- what is the temporal scale we will work on
- What are the boundary conditions or assumptions
- Which dimensions will we take into account (which processes will we consider)
- How will we describe the dimensions


| building block  |  decision |
|---|---|
| Geographic scale |  Transect (line) |
| temporal scale |  Long term average (at least year-based), and all data input should span same timespan |
| Assumption | 'Greenness' of the land directly depends on the water deficit (or, the comparison of PET with precipitation)  |
| Dimensions | We'll consider water deficit as independent variable, NPP as dependent variable |
| Dimension description | TerraClimate for the deficit, NPP from MODIS Imagery |




> step 2: Define the spatial unit, and import the relevant layers



The spatial unit in our case is a 'Line': we can define this using the function ee.Geometry.LineString, which just needs the beginning and end coordinates as (LONG,LAT) pairs. 

Next, we can plot the transect on the map. 

```javascript
// defining the variable 'transect' as the gradient we want to investigate:  
var transect = ee.Geometry.LineString([[-123, 46], [-120, 46]]);
Map.addLayer(transect, {color: 'FF0000'}, 'transect');
```

Now, we can import the Image(collections): the NPP from MODIS satellite and the water Deficit from the Terraclimate project

```javascript

var NPP = ee.ImageCollection('UMT/NTSG/v2/MODIS/NPP')
                  .filter(ee.Filter.date('2017-01-01', '2017-12-31'));
var npp = NPP.select('annualNPP');
var nppVis = {
  min: 0.0,
  max: 20000.0,
  palette: ['bbe029', '0a9501', '074b03'],
};
Map.addLayer(npp, nppVis, 'NPP');
//Because npp is an imagecollection (consisting of only 1 image) we want to select -and continue with -  only that image: 
var nppImage = npp.first();


var climateset = ee.ImageCollection('IDAHO_EPSCOR/TERRACLIMATE')
                  .filter(ee.Filter.date('2017-01-01', '2017-12-31'));
//we can directly use the climate water deficit (one of the bands):
var deficit = climateset.select('def');
print(deficit);


```

**print(deficit) function gives you an overview of the content of the ImmageCollection 'deficit'. How many images (features) are in the Immagecollection, why? Does the npp variable have the same amount of images?**



Indeed, we'll have to somehow summarize the information of the images in 'deficit' to obtain one image. Luckily, there is a [function](https://developers.google.com/earth-engine/guides/reducers_image_collection) that helps us.


```javascript
var meandeficit = deficit.reduce(ee.Reducer.mean());
Map.addLayer(meandeficit, {min: 0, max: 3000}, 'deficit');
```





> step 3: Plot the values of the dependent and independent variables along the transect

Now that we have the data, we can make a plot showing how npp and deficit varies when moving along the transect from west to east. 

```javascript


//the nppImage has some 'gaps'(the mask), we'll need to set those values to zero: 
var nppwzero = nppImage.unmask(0);

// now, we add explicit coordinates to the npp and deficit images, so that we can then link them to the transect coordinates. 
// Define a pixel coordinate image and add it to our two images of interest
var latLonImg = ee.Image.pixelLonLat();
var nppImage = nppwzero.addBands(latLonImg);
var meandeficitImage = meandeficit.addBands(latLonImg);

// Now we can summarize (Reduce) npp and coordinate bands by transect line; get a dictionary with
// band names as keys, pixel values as lists.
var nppTransect = nppImage.reduceRegion({
  reducer: ee.Reducer.toList(),
  geometry: transect,
  scale: 1000,
});

print(nppTransect);



var deficitTransect = meandeficitImage.reduceRegion({
  reducer: ee.Reducer.toList(),
  geometry: transect,
  scale: 1000,
});

print(deficitTransect);




//OK, so far so good: now we have two objects containing lists of deficits, npp and coordinates: once we sort them, we can plot them: 
// Define the chart and print it to the console.
// Get longitude and elevation value lists from the reduction dictionary.
var lon = ee.List(deficitTransect.get('longitude'));
var lat = ee.List(deficitTransect.get('latitude'));
var deficitlist = ee.List(deficitTransect.get('def_mean'));
var npplist = ee.List(nppTransect.get('annualNPP'));


// Sort the longitude and elevation values by ascending longitude.
var lonSort = lon.sort(lon);
var latSort = lat.sort(lat);
var deficitSort = deficitlist.sort(lonSort);
var nppSort = npplist.sort(lonSort);

var chart = ui.Chart.array.values({array: deficitSort, axis: 0, xLabels: lonSort})
                .setOptions({
                  title: 'deficit Profile Across Longitude',
                  hAxis: {
                    title: 'Longitude',
                    viewWindow: {min: -122.7, max: -120.1},
                    titleTextStyle: {italic: false, bold: true}
                  },
                  vAxis: {
                    title: 'deficit (mm)',
                    titleTextStyle: {italic: false, bold: true}
                  },
                  colors: ['1d6b99'],
                  lineSize: 3,
                  pointSize: 0,
                  legend: {position: 'none'}
                });
print(chart);
var chart = ui.Chart.array.values({array: nppSort, axis: 0, xLabels: lonSort})
                .setOptions({
                  title: 'npp Profile Across Longitude',
                  hAxis: {
                    title: 'Longitude',
                    viewWindow: {min: -122.7, max: -120.1},
                    titleTextStyle: {italic: false, bold: true}
                  },
                  vAxis: {
                    title: 'NPP ',
                    titleTextStyle: {italic: false, bold: true}
                  },
                  colors: ['1d6b99'],
                  lineSize: 3,
                  pointSize: 0,
                  legend: {position: 'none'}
                });
print(chart);


Map.addLayer(transect, {color: 'FF0000'}, 'transect');


```

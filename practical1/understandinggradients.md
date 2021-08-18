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


var climateset = ee.ImageCollection('IDAHO_EPSCOR/TERRACLIMATE')
                  .filter(ee.Filter.date('2017-01-01', '2017-12-31'));
//we can directly use the climate water deficit (one of the bands):
var deficit = climateset.select('def');
print(deficit);
Map.addLayer(deficit, {min: 0, max: 3000}, 'deficit');

```

**print(deficit) function gives you an overview of the content of the ImmageCollection 'deficit'. How many images (features) are in the Immagecollection, why? Does the npp variable have the same amount of images?**



Indeed, we'll have to somehow summarize the information of the images in 'deficit' to obtain one image. Luckily, there is a [function](https://developers.google.com/earth-engine/images/Reduce_ImageCollection.png) that helps us.



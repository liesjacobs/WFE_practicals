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
| temporal scale |  Long term average (at least year-based) |
| Assumption | we'll consider local effects of climate and geomorphology on land cover  |
| Dimensions | we'll consider topography, precipitation and temperature as independent variables, NPP as dependent variable |
| Dimension description | SRTM DEM, worldClim dataset on P and T, NPP from LANDSAT |


> step 2: Define the spatial unit, and import the relevant layers

The spatial unit in our case is a 'Line': we can define this using the function ee.Geometry.LineString, which just needs the beginning and end coordinates as (LONG,LAT) pairs. 

Next, we can plot the transect on the map. 

```javascript
// defining the variable 'transect' as the gradient we want to investigate:  
var transect = ee.Geometry.LineString([[-123, 46], [-120, 46]]);
Map.addLayer(transect, {color: 'FF0000'}, 'transect');
```

Now, we can import the Image(collections). We'll start with an easy one: the SRTM DEM

```javascript
// Now we can import the Image(collections)
var SRTMDEM = ee.Image('CGIAR/SRTM90_V4');
var elevation = SRTMDEM.select('elevation');
```

Do you understand this last line? If this is cryptic: try print(SRTMDEM); to print the information on this Image to the console, this might clarify this last line of code. 

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
| Assumption | 'Greenness' of the land directly depends on the water deficit (or, the comparison of PET with precipitation) , which in turn depends on rainfall and Potential evapotranspiration (thus Temperature), which in turn is determined by a strong topographic boundary (the mountain range) |
| Dimensions | We'll consider water deficit, rainfall, temperature and elevation as independent variables, NPP as dependent variable |
| Dimension description | SRTM DEM, TerraClimate, NPP from LANDSAT |


==> For the purpose of this exercise, we'll further simplify: We'll start with simply investigating the relationship between water-deficit and primary production

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
var var climateset = ee.ImageCollection('IDAHO_EPSCOR/TERRACLIMATE')
                  .filter(ee.Filter.date('2017-07-01', '2017-08-01'));
//we can directly use the climate water deficit proposed:
var deficit = climateset.select('def');
```

Do you understand this last line? If this is cryptic: try print(climateset); to print the information on this Image to the console, this might clarify this last line of code. 


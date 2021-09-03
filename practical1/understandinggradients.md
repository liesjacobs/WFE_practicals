### Exercise 3: Understanding the Gradient : how process influences form

In this exercise we will actually *use* data from earth engine to gain insight in a real-life question: 
How can we explain the remarkable gradient in land cover (and related agricultural practices) along the West-Coast of the USA (see slides 32-33 course 1)





> step 1: make a new Script in Earth engine, and give it an appropriate name (e.g. transects)





Now we can think about the building blocks of the analysis (see slide 45, course 1): 
- what Geographic scale – spatial unit is appropriate
- what is the temporal scale we will work on
- What are the boundary conditions or assumptions
- Which dimensions will we take into account (which processes will we consider)
- How will we describe the dimensions¬


| building block  |  decision |
|---|---|
| Geographic scale |  Transect (line) |
| temporal scale |  all data input should span same timespan |
| Assumption | The different landcovers on such a short transect are due to either a steep temperature gradient, or a steep precipitation gradient, either can be induced by the topographic barrier |
| Dimensions | We'll winter and summer temperature and yearly precipitation |
| Dimension description | LANDSAT band 10 for temperature, CHIRPS for precipitation, a local DEM for topography |

¬


> step 2: Define the spatial unit, and import the relevant layers



The spatial unit in our case is a 'Line': we can define this using the function ee.Geometry.LineString, which just needs the beginning and end coordinates as (LONG,LAT) pairs. 

Next, we can plot the transect on the map. ¬

```javascript
// defining the variable 'transect' as the gradient we want to investigate:  
var endpoint = [-118.821944, 46.527222];
var startpoint = [-123.416667, 46.783333];
var transect = ee.Geometry.LineString([endpoint, startpoint]);
Map.addLayer(transect, {color: 'FF0000'}, 'transect');
```

Now, we can import the Image(collections) we need

```javascript
// Get brightness temperature data for 1 year: se select band 10 of landsat8, convert kelvin to celcius and define the dates of aquisition
var landsat8Toa = ee.ImageCollection('LANDSAT/LC08/C01/T1_TOA');
var temperature = landsat8Toa.filterBounds(transect)
    .select(['B10'], ['temp'])
    .map(function(image) {
      // Kelvin to Celsius.
      return image.subtract(273.15)
          .set('system:time_start', image.get('system:time_start'));
    });
    
//import elevation:
var elevation = ee.Image('USGS/NED');  // Extract the elevation profile.

// let's add precipitation ass well (mm/pentad, or mm/5days), similar as temperature
var chirps = ee.ImageCollection("UCSB-CHG/CHIRPS/PENTAD");
var chirpsprecip = chirps.filterBounds(transect)
    .select(['precipitation'], ['previp'])
    .set('system:time_start', chirps.get('system:time_start'));
    
```

> step 3: prepare the data for plotting on a graph

Now that we have all the image(collections), we can 'reduce' the data, so that we have the winter and summer temperature along the transect, the total precipitation and the topography, and we can combine all this data into one *new image*. 

```javascript
//selecting a year worth of data for CHIRPS and sum all the data (so total yearly precipitation)
var chirpsprecipselect = chirpsprecip.filterDate('2014-01-01', '2014-12-31')
                          .reduce(ee.Reducer.sum())
                          .select([0], ['yearprec']);
                          
// Calculate bands for seasonal temperatures and elevations; c
var summer = temperature.filterDate('2014-06-21', '2014-09-23')
    .reduce(ee.Reducer.mean())
    .select([0], ['summer']);
var winter = temperature.filterDate('2013-12-21', '2014-03-20')
    .reduce(ee.Reducer.mean())
    .select([0], ['winter']);

//join all the data into one new image: 
// we first make a list describing the distance from the startingpoint:
var startingPoint = ee.FeatureCollection(ee.Geometry.Point(startpoint));
var distance = startingPoint.distance(450000);
//now we add all the bands to the distance list:
var image = distance.addBands(elevation).addBands(winter).addBands(summer).addBands(chirpsprecipselect);

```



OK: now we have all ingredients to sort the information and plot it all in one chart 

```javascript
// Extract band values along the transect line: convert the image information into an array (list).
var array = image.reduceRegion(ee.Reducer.toList(), transect, 1000)
                 .toArray(image.bandNames());

// Sort points along the transect by their distance from the starting point.
var distances = array.slice(0, 0, 1);
array = array.sort(distances);

// Create arrays for plotting in a figure.
var elevationAndTempAndPrecip = array.slice(0, 1);  // For the Y axis.
// Project distance slice to create a 1-D array for x-axis values.
var distance = array.slice(0, 0, 1).project([1]);


```
> step 3: prepare the data for plotting on a graph  


```javascript
// Generate and style the chart.
var chart = ui.Chart.array.values(elevationAndTempAndPrecip, 1, distance)
    .setChartType('LineChart')
    .setSeriesNames(['Elevation', 'Winter 2014', 'Summer 2014', 'Precipitation 2014'])
    .setOptions({
      title: 'Elevation, temperatures and precipitation along transect',
      vAxes: {
        0: {
          title: 'Average seasonal temperature (Celsius)'
        },
        1: {
          title: 'Elevation (meters, blue) or precipitation (mm, Green)',
          baselineColor: 'transparent'
        }
      },
      hAxis: {
        title: 'Distance from starting points (m)'
      },
      interpolateNulls: true,
      pointSize: 0,
      lineWidth: 1,
      // Our chart has two Y axes: one for temperature and one for elevation/precip.
      // Y axis, which we do here:
      series: {
        0: {targetAxisIndex: 1},
        1: {targetAxisIndex: 0},
        2: {targetAxisIndex: 0}, 
        3: {targetAxisIndex: 1},
      }
    });

print(chart);
Map.setCenter(-121, 46, 7);
Map.addLayer(elevation, {min: 4000, max: 0});
Map.addLayer(transect, {color: 'FF0000'});

```



*Note that you can click on the small arrow on the right upper corner of your graph to maximize the window

##**Congrats: you can now analyze multiple layers at the same time on the same graph: is the result what you expected**? 

<nav>
  <ul>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.html">Practical 1: exercise 1</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/exploring.html">Practical 1: exercise 3</a></li>
      <li><strong>Practical 1: exercise 3</strong></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/"><b>Back to Overview Page</b></a></li>
  </ul>
</nav>

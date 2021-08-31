# Welcome to the Second practical. 

In this practical we will be using a combination of Google Earth Engine-QGIS-R to understand global biodiversity patterns. No need to worry, we'll tackle it step by step. It is however essential that you found your way trough the [first practical](https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.html) as we will start with getting (some of our) data there. 

## Step 1: Required softwares and datasets: overview

###**Softwares** 
As mentioned on the [starting page](https://liesjacobs.github.io/World-Food-and-Ecosystems/), you'll need QGIS, Rstudio and a working account for [code editor](code.earthengine.google.com/).

###**Datasets**

We'll use following datasets: 

| Dataset      | Type | Source     |Access point     |
| :---        |    :---    |          :---  |         :---  |
| Mammal species richness - Global      | Raster       | Jenkins et al. 2015  |[biodiversity.org](https://biodiversitymapping.org/wp-content/uploads/2018/12/Mammal_maps_hi_res_2018_12d16.zip)   |
| NDVI map - Global   | Raster        | Modis Imagery      |Google Earth Engine: see below     |
| Watershed delineations - Global  | Vector        | WWF      |Google Earth Engine: see below     |



## Step 2: accessing the data

The easiest dataset to access is the raster file for Mammal Species Richness: just clicking on the link in the table should result in an immediate download of a ZIP file. Unpacking this gives you access to a raster file. 

For the two other maps we can use Google Earth Engine to access them. 

We'll start with visualizing and downloading the NDVI map: Google Earth Engine allow to upload any *Image* you make to your google drive: once on your drive, you can download it from there. 

The whole google earth engine code is here below, with each of the lines commented: make sure you understand what all the different parts are for, what they do, and try to execute the code yourself using your own google earth engine account: 

```javascript

/// we define the area for which we want to download data:
var clip = 
    ee.Geometry.Polygon(
        [[[-180, 60],
          [-180, -60],
          [180, -60],
          [180, 60]]], null, false);


/// we define the dataset (ImageCollection) we are interested in, and already filter a few years from it:
var dataset = ee.ImageCollection('MODIS/006/MOD13A2')
                  .filter(ee.Filter.date('2015-01-01', '2018-12-31'));
                  
/// the MODIS image collection we just defined contained much more than only NDVI. We can check what is in this dataset by using *print*:
print(dataset);
// the info on what is in the datset now appears in the console, where you can click on the item and explore


/// so let's just select NDVI
var ndvi = dataset.select('NDVI');
print(ndvi);
// you can see in the console, that it is still an image collection, because it contains one NDVI image per 16 days!

// so we'll have to take the average over the whole set:
var mean = ndvi.reduce(ee.Reducer.mean());
print(mean);
// indeed: taking the average *reduces* the image collection to an Image: this we can export to our drive
// but... let's first visualize:-)


// define the minimum, maximum and the colour pallette: 
var ndviVis = {
  min: -1000,
  max: 9000.0,
  palette: [
    'FFFFFF', 'CE7E45', 'DF923D', 'F1B555', 'FCD163', '99B718', '74A901',
    '66A000', '529400', '3E8601', '207401', '056201', '004C00', '023B01',
    '012E01', '011D01', '011301'
  ],
};

//center the map, and add the ndvi map: 
Map.setCenter(6.746, 46.529, 2);
Map.addLayer(ndvi, ndviVis, 'NDVI');




// Export our 'mean' to your google drive: we have to define the region (clip), the scale: here we take 5km at the equator, and give it a name
Export.image.toDrive({
  image: mean,
  description: 'meanNDVI_MODIS',
  scale: 5000,
  region: clip,
  fileFormat: 'GeoTIFF'
});
// after running this it should appear in your 'tasks' here to the right: click on 'run'
```
After running this code, a geo-tiff file (type of raster file) should load in your google drive: from here you can download it to your PC:-). 







But now that you know the basics, let's explore its functionalities: 
[![follow-me](https://github.com/liesjacobs/World-Food-and-Ecosystems/blob/gh-pages/Picture1.png)](https://liesjacobs.github.io/World-Food-and_Ecosystems/practical1/exploring.html)




<nav>
  <ul>
    <li><strong>Practical 1: exercise 1</strong></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/exploring.html">Practical 1: exercise 2</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/understandinggradients.html">Practical 1: exercise 3</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/"><b>Back to Overview Page</b></a></li>
  </ul>
</nav>



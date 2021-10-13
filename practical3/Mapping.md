# Step 3: Mapping and geo-processing


>Let's start off easy, and build a map of the raccoon sightings in Belgium: 
>>Load all the data in QGIS: the video below shows how you can make a map of the vector data you collected:


<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132331875-35103196-e929-4c60-99fe-9b05740ba3c8.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


>Next step in QGIS is to use the grids we made earlier and summarize the data per grid. Each of these things can be achieved through a different function in QGIS
>>How many raccoon sightings? --> *Count points per polygon*
>>Average topographic diversity? -->*Zonal statistics*
>>total river length per polygon grid cell? -->*Sum of line lenght*

The videos below show you how you can implement these different functions: 

### Count points per polygon


<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132332865-8542bef2-911c-4f71-b1d7-a4d546962aab.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


### Average topographic diversity 


<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132332818-bc5a061b-ec10-4fab-af89-59d311680b1d.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

### Sum of line length


<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/132332926-3511c33e-b4bd-436d-a79d-d5f699288920.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>


***

Note that this last video also demonstrates how to export the data as a csv. This we do to make sure we can read the results of our processing in Rstudio, where we will do the [final analysis](https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/Analysis.html)


<nav>
  <ul>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.html">Practical 1: exercise 1</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/exploring.html">Practical 1: exercise 2</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/understandinggradients.html">Practical 1: exercise 3</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical2/intro.html">Practical 2: exercise 1</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical2/QGIS.html">Practical 2: exercise 2</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical2/Rstudio.html">Practical 2: exercise 3</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical3/intro.html">Practical 6: Problem description</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical3/API.html">Practical 6: Data Collection</a></li>
    <li><strong>Practical 6: Mapping and spatial processing</strong></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/practical3/Analysis.html">Practical 6: Analysis</a></li>
    <li><a href="https://liesjacobs.github.io/World-Food-and-Ecosystems/"><b>Back to Overview Page</b></a></li>
  </ul>
</nav>

# Welcome to the Third practical. 


Congratulations, you have come a very long way...

In the previous two sessions, we have focessed a lot on implementing command-line based data retrieval and analysis, and tried to move away from a point-and-click approach. 

This was not without reason:-). 

Command-line-based tools allow repetition, (parallel) processing, automation of algorithms, and automatic data retrieval. 

>This is often done through an API, or Application Programmin Interface, or a set of conventions/rules/protocols that can be used so that one application (e.g. QGIS) can easily communicate with another (e.g. open street map). 

Although the term might be new to you, the concept itself is not. 

- e.g. try typing 'weather Amsterdam' in Google: google will understand that these two strings mean you want to search for a weather forcast and will use this to construct one based on 3rd party weather providers. 
- Actually... the exercises we have done in GEE is a good example of an API implementation: GEE knows and recognizes conventions (e.g. map.AddLayer(), ee.ImageCollection()....) and knows how to use these to perform tasks

In this last practical we will  we will be using a combination of Google Earth Engine-QGIS-R to analyse the occurrence of Raccoons in Belgium. We will use API implementations in all three tools to access data, and we'll do a processing step in QGIS and some postprocessing in Rstudio. 

![flow](https://user-images.githubusercontent.com/89069805/132313591-66560e0a-57de-4a5b-ad67-5e9312f9ebfd.png)

It is however essential that you found your way trough the [first practical](https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.html) as well as the [second practical](https://liesjacobs.github.io/World-Food-and-Ecosystems/practical2/intro.html) as this last practical builds upon this. 


## Step 1: Required softwares and datasets: overview

### **Softwares** 

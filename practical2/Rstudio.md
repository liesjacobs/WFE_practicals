# Exercise 3: exporting the attribute data and importing in Rstudio

So... we want to export the attribute data of our shapefile to a file that can be imported in Rstudio, e.g. a .csv file. 

Luckily, that's quite straightforward: 

<video style="width:100%" controls>
  <source src="https://user-images.githubusercontent.com/89069805/131507742-01689c6d-726c-4cfa-9853-ea126a24a054.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

https://user-images.githubusercontent.com/89069805/131507742-01689c6d-726c-4cfa-9853-ea126a24a054.mp4






### Great: so now we can shift to Rstudio

Open Rstudio. If all goes well, it should look something like this: 

![Rstudio_Home](https://user-images.githubusercontent.com/89069805/131488428-fe3591d5-2cd0-4107-8dd1-84b4aafe883b.png)

With on the left the console (where you execute single commands), on the top right a panel where you can see the variables in the 'environment'. In the bottom right you can see the plots you make, but also e.g. the packages that are installed, or the help function. 

We now have to do two things: 

1. Import the dataset
2. Build an R script


### Importing the .csv file we just made



https://user-images.githubusercontent.com/89069805/131488949-4c653f75-fd4a-4cb1-b619-feae62826521.mp4


Depending on the settings of your PC, you might need to adjust the decimal notation, or the seperator. 
If all is well, you now see the attribute information in the environment. 



### Building a script

Now we can start analyzing the data. The first thing you need to do is build an empty R file where you will later put the commands you'll use for analysis. 



https://user-images.githubusercontent.com/89069805/131489386-bf1b4aee-c1bc-42d3-a1fa-afc8397c0b7e.mp4



We can add simple code, as illustrated in the video below 


https://user-images.githubusercontent.com/89069805/131489891-e0210044-50ad-4361-9fea-1b8e095dbbc7.mp4


The plot is a bit ugly, so we can pimp it, and also plot the regression line. 
Copy paste the code below and execute it yourself: 

```r
# this is the file where we will list the commands needed for the analysis
# using a hashtag = comments 

# now we can build simple code, to do some analysis

#cleaning data
attributesNDVI_Richness<-na.omit(attributesNDVI_Richness)
attach(attributesNDVI_Richness)

# first, let's plot
library(scales) # if you get an error here, first install package 'scales' using install.packages('scales')
plot(NDVImean, richnessme, xlab = "NDVI", ylab = "Mammal richness", col=alpha("green",0.3), pch = 16)

# then build a regression: 
regression <- lm(richnessme~NDVImean, data = attributesNDVI_Richness)
summary(regression)


# plot regression line on scatterplot
abline(regression, col="black", lwd=2)

text(1000,150, paste("r squared is ", round(summary(regression)$r.squared,2)))
text(1000,140, paste("p-value of NDVI is ", summary(regression)$coefficients[8]))

```


After the execution, you should get something like this: 

![example](https://user-images.githubusercontent.com/89069805/131496702-b8d0af27-b702-4175-8525-1ce44975cc2b.png)

# Step 4: Analysis

Now that we have summarized all the ancillary data to our regular grid, we can import the csv in R and do some simple visualizations

```r
#loading the data: adjust the path name and the file name to your specific file: 
clipgridbel <- read.csv("C:/Users/lhjacob/OneDrive - UvA/UvA-Education/teaching/WFE/coursedocs2021/practical3/grid005_topodiv_raccoons_riverlength.csv")

#does the number of raccoons depend on the mean topographic diversity? 
plot(clipgridbel$NUMPOINTS~clipgridbel$Topomean)
#how about the number of raccoons vs. the river length in grid
plot(clipgridbel$NUMPOINTS~clipgridbel$LENGTH)


#both seem a bit inconclusive: this makes sense, we are plotting the number of sightings, but this might
#depend a lot on potential observation biases. 

#let's take a more basic approach: are cells with raccoons characterized by a higher topogr diversity? 
#first convert numpoints attribute: everything that is larger than zero (i.e. at least one raccoon) will be coded as 1
clipgridbel$NUMPOINTS[which(clipgridbel$NUMPOINTS>0)]<-1
boxplot(clipgridbel$Topomean~clipgridbel$NUMPOINTS, outline = F, col=c("green", "pink"), xlab="presence of raccoons", ylab="mean topographic index")


#and what about the rivers? 
boxplot(clipgridbel$LENGTH~clipgridbel$NUMPOINTS, outline = F, col=c("green", "pink"), xlab="presence of raccoons", ylab="total river length")
```


## Based on this analysis, which statistical tests would you do? 

## Are the effects you see real? Or are there other factors we did not consider? 

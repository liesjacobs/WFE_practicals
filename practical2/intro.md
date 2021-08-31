# Welcome to the Second practical. 

In this practical we will be using a combination of Google Earth Engine-QGIS-R to understand global biodiversity patterns. No need to worry, we'll tackle it step by step. It is however essential that you found your way trough the [first practical] (https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.html) as we will start with getting (some of our) data there. 

## Step 1: Required softwares and datasets: overview

###**Softwares** 
As mentioned on the [starting page] (https://liesjacobs.github.io/World-Food-and-Ecosystems/), you'll need QGIS, Rstudio and a working account for [code editor](code.earthengine.google.com/).

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
The Google Earth Engine interface, as you see it above, runs on JavaScript. It might seem scary to be confronted with a new (and at times cryptic) language, but no worries: we'll go step by step. 

To access, explore and use Google Earth Engine, only a basic understanding of JavaScript suffices. As we saw in class, the basic building blocks of writing code (in python, R, Javascript...) is (i) the identification of the necessary variables, (ii) the identification of the appropriate functions, (iii) understanding which input parameters these functions require. 

Of course, although the building blocks are similar, the syntax can differ quite a bit. Some key tips and tricks for JavaScript are listed here (source: <a href="https://docs.google.com/document/d/1ZxRKMie8dfTvBmUNOO0TFMkd7ELGWf3WjX0JvESZdOE/edit" target="_blank">Earth Engine 101 Beginner's Curriculum</a>.)


```javascript

// Line comments start with two forward slashes. Like this line.

/* Multi-line comments start with a forward slash and a star,
and end with a star and a forward slash. */
```

Variables are used to store objects and are defined using the keyword **var**.
```javascript

var theAnswer = 42;
```
string objects start and end with a single quote
```javascript
var myVariable = 'I am a string';

// string objects can also use double quotes, but don't mix and match
var myOtherVariable = "I am also a string";
```

```javascript
Statements should end in a semi-colon, or the editor complains.

var test = 'I feel incomplete...'
var test2 = 'I feel complete!';
```

Passing function parameters and using lists: 
```javascript
// Parentheses are used to pass parameters to functions
print('This string will print in the Console tab.');

/* Square brackets are used for items in a list.
The zero index refers to the first item in a list*/
var myList = ['eggplant','apple','wheat'];
print(myList[0]); // would print 'eggplant' because JavaScript starts counting from 0 (and not from 1, like R)
```

Using dictionaries
```javascript

// Curly brackets (or braces) can be used to define dictionaries (key:value pairs).
var myDict = {'food':'bread', 'color':'red', 'number':42};

// Square brackets can be used to access dictionary items by key.
print(myDict['color']);

//Or you can use the dot notation to get the same result.
print(myDict.color);
```

Functions can be defined as a way to reuse code and make it easier to read.
```javascript
var myHelloFunction = function(string) {
  return 'Hello ' + string + '!';
};
print(myHelloFunction('world'));



```


<p style="color:blue;" "font-weight:bolder;">Question 1.1. In this last function, what is the input that the function needs? </p>



In this course, you won't have to write code yourself: we'll simply adjust existing pieces of code, to get into the modus operandus. If you want to learn more, [this source from the science park study group](https://scienceparkstudygroup.github.io/Intro-Google-Earth-Engine-lesson/) is an excellent starting point. 


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



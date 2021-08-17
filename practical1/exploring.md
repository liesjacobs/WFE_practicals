# Welcome to the first practical. 

In this practical we will be exploring the datasets and functionalities of Google Earth Engine. If all is well, you have created an account on earth engine by following the instructions on [the starting page](https://liesjacobs.github.io/World_Food-and_Ecosystems/)


## Step 3: exploring the functionalities

Now that we know more or less how it looks, let's use it. 
If at any point your lost on the basic JavaScript commands, go [back](https://liesjacobs.github.io/World-Food-and-Ecosystems/practical1/intro.md)

> Exercise 1: plotting the biome map of the world and exploring its values. 

Copy this piece of code in the 'script' panel of the earth engine GUI. 

```javascript

// first we retrieve the Image (the raster dataset) from the server and declare the variable
var biomes = ee.Image("OpenLandMap/PNV/PNV_BIOME-TYPE_BIOME00K_C/v01");

// but what have we done exactly? Let's see what it is in this 'Image'. 
print(biomes);

```

Save the file (e.g. name it 'BiomePlotting') and run it. 

If all goes well, you should see some basic information about the image *printed* in the console: how many bands does this Image have?



```javascript
var visualization = {
  bands: ['biome_type'],
  min: 1.0,
  max: 32.0,
  palette: [
    "1c5510","659208","ae7d20","000065","bbcb35","009a18",
    "caffca","55eb49","65b2ff","0020ca","8ea228","ff9adf",
    "baff35","ffba9a","ffba35","f7ffca","e7e718","798649",
    "65ff9a","d29e96",
  ]
};

Map.centerObject(dataset);

Map.addLayer(dataset, visualization, "Potential distribution of biomes");

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

In this course, you won't have to write code yourself: we'll simply adjust existing pieces of code, to get into the modus operandus. If you want to learn more, [this source from the science park study group](https://scienceparkstudygroup.github.io/Intro-Google-Earth-Engine-lesson/) is an excellent starting point. 


But now that you know the basics, let's explore its functionalities: 
[![follow-me](https://github.com/liesjacobs/World-Food-and-Ecosystems/blob/gh-pages/Picture1.png)](https://github.com/liesjacobs/World-Food-and-Ecosystems/edit/gh-pages/practical1/exploring.md)



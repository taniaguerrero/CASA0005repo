# Advanced raster analysis

## Learning objectives

1. Explain and execute appropraite pre-proessing steps of raster data
3. Replicate published methodologies using raster data
4. Design new R code to undertake further analysis 

## Introduction

Within this practical we are going to be using data from the Landsat satellite series provided for free by the United States Geological Survey (USGS) to replicate some published methods. Landsat imagery is the longest free temporal image repository of consistent medium resolution data. It collects data at each point on Earth each every 16 days (temporal resolution) in a raster grid composed of 30 by 30 m cells (spatial resolution). Geographical analysis and concepts are becoming ever more entwined with remote sensing and Earth observation. Back when I was an undergraduate there was specific software for undertaking certain analysis, now you can basically use any GIS. I see remote sensing as the science behind collecting the data with spatial data analysis then taking that data and providing meaning. So whilst i'll give a background to Landsat data and remote sensing, this practical will focus on more advanced methods for analysing and extracting meaning from raster data.

### Remote sensing background (required)

* Landsat is raster data
* It has pixels of 30 by 30m collected every 16 days with global coverage
* As humans we see in the visible part of the electromagnetic spectrum (red-green-blue) Landsat takes samples in these bands and several more to make a spectral sigature for each pixel (see image below)
* Each band is provided as a seperate ```.TIFF``` raster layer

<img src="prac7_images/specsig.jpg" width="500pt" style="display: block; margin: auto;" />

Later on we will compute temperature from the Landsat data, whilst i refer to and explain each varaiable created don't get overwhelmed by it, take away the process of loading and manipulating raster data in R to extract meaningful information. An optional remote sensing background containing additional information can be found at the end of this practical should you wish to explore this further.

## Data

### Shapefile

The shapefile of Manchester is available on my GitHub account:

https://github.com/andrewmaclachlan/CASA0005book/tree/master/prac7_data

### Raster data (Landsat)

To access the Landsat data we will use in this practical you can either:

(a) Sign up for a free account at: https://earthexplorer.usgs.gov/. 
(b) Use the Landsat data provided on Moodle --- this will be available only if the earth explorer website is down

To download the data:

1. Search for Manchester in the address/place box and select it. 
2. Select the date range between the 12/5/2019 and 14/5/2019 --- it's a US website so check the dates are correct.
3. Click dataset and select Landsat, then Landsat Collection 1 Level-1, check Landsat 8 (level 2 is surface reflectance --- see optional remote sensing background)
4. Click results, there should be one image, download it..it might take a while
5. Landsat data comes zipped twice as a ```.tar.gz```. Use 7Zip to extract it once to get to a ```.tar``` then extract again using 7Zip and files should appear.

## Processing raster data

### Loading

Today, we are going to be using a Landsat 8 raster of Manchester. The vector shape file for Manchester has been taken from an ESRI repository. 

6. Let's load the majority of packages we will need here. 


```r
## listing all possible libraries that all presenters may need following each practical
library(sp)
library(raster)
library(rgeos)
library(rgdal)
library(rasterVis)
library(ggplot2)
```

7. Now let's list all our Landsat bands except band 8 (i'll explain why next) along with our study area shapefile. Each band is a seperate ```.TIF``` file.






































































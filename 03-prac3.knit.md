# Rasters, descriptive statistics and interpolation

## Learning outcomes

By the end of this practical you should be able to:

* Load, manipulate and interpret raster layers
* Observe and critique different descriptive data manipulation methods and outputs
* Exceute interpolation of points to a raster layer
* Construct a methodology for comparing raster datasets

## Introduction 

This practical is composed of three parts. To start with we're going to load some global raster data into R. In the second part we extract data points (cities and towns) from this data and generate some descriptive statistics and histograms. In the final section we explore interpolation using point data. 

## Part 1 rasters

So far we've only really considered vector data. Within this practical we will explore some raster data sources and processing techniques. If you recall rasters are grids of cell with individual values. There are many, many possible sources to obtain raster data from as it is the data type used for the majority (basically all) of remote sensing data.

### WorldClim data

To start with we are going to use WorldClim data --- this is a dataset of free global climate layers (rasters) with a spatial resolution of between 1$km^2$ and 240$km^2$.

1. Download the data from: http://worldclim.org/version2

2. Select any variable you want at the 5 minute second resolution. What is a 5 minute resolution i hear you ask? Well, this geographic reference system treats the globe as if it was a sphere divided into 360 equal parts called degrees. Each degree has 60 minutes and each minute has 60 seconds. Arc-seconds of latitude remain almost constant whilst arc-seconds of longitude decrease in a trigonometric cosine-based fashion as you move towards the Earth's poles....

<img src="prac3_images/arcseconds.jpg" width="400pt" style="display: block; margin: auto;" />

If you are still a bit confused by coordiate reference systems have a look at the following:
* https://communityhub.esriuk.com/geoxchange/2012/3/26/coordinate-systems-and-projections-for-beginners.html
* https://en.wikipedia.org/wiki/Spatial_reference_system

3. Unzip and move the data to your project folder. Now load the data. We could do this individually....


```r
library(raster)
jan=raster("prac3_data/wc2.0_5m_tavg_01.tif")
# have a look at the raster layer jan
jan
```

```
## class      : RasterLayer 
## dimensions : 2160, 4320, 9331200  (nrow, ncol, ncell)
## resolution : 0.08333333, 0.08333333  (x, y)
## extent     : -180, 180, -90, 90  (xmin, xmax, ymin, ymax)
## crs        : +proj=longlat +datum=WGS84 +no_defs +ellps=WGS84 +towgs84=0,0,0 
## source     : C:/Users/ucfnmac/OneDrive - University College London/Teaching/CASA0005repo/prac3_data/wc2.0_5m_tavg_01.tif 
## names      : wc2.0_5m_tavg_01 
## values     : -46.697, 34.291  (min, max)
```

4. Then have a quick look at the data


```r
plot(jan)
```

<img src="03-prac3_files/figure-html/unnamed-chunk-3-1.png" width="672" />

5. A better and more efficient way is to firstly list all the files stored within our directory


```r
listfiles <- list.files("prac3_data/", ".tif")

#have a look at the file names 
listfiles
```

```
##  [1] "wc2.0_5m_tavg_01.tif" "wc2.0_5m_tavg_02.tif" "wc2.0_5m_tavg_03.tif"
##  [4] "wc2.0_5m_tavg_04.tif" "wc2.0_5m_tavg_05.tif" "wc2.0_5m_tavg_06.tif"
##  [7] "wc2.0_5m_tavg_07.tif" "wc2.0_5m_tavg_08.tif" "wc2.0_5m_tavg_09.tif"
## [10] "wc2.0_5m_tavg_10.tif" "wc2.0_5m_tavg_11.tif" "wc2.0_5m_tavg_12.tif"
```

6. Then load all of the data straight into a raster stack. A raster stack is a collection of raster layers with the same spatial extent and resolution.










































































afrilearndata • afrilearndata















Toggle navigation





[afrilearndata](index.html)
0\.0\.0\.9003



* 
* [Reference](reference/index.html)
* [Changelog](news/index.html)


* 











afrilearndata
=============




afrilearndata provides small African spatial datasets to help with learning and teaching of spatial techniques and mapping.


The motivation is to provide analysts based in Africa with more easily relateable example datasets. More generally we aim to support the growth of R and mapping in the continent. Part of the [afrimapr](https://afrimapr.github.io/afrimapr.website/) project providing R building blocks, training and community.



Installation
------------


Install the development version of afrilearndata with:



```


    # install.packages("remotes") # if not already installed
    
    remotes::[install_github](https://remotes.r-lib.org/reference/install_github.html)("afrimapr/afrilearndata")
    
    [library](https://rdrr.io/r/base/library.html)(afrilearndata)
```



Datasets
--------


The package contains the following objects


1. `africontinent` polygons, continent outline including madagascar
2. `africountries` polygons, 51 country boundaries
3. `afrihighway` lines, trans African highway network (100 lines)
4. `africapitals` points, 51 capital cities
5. `afriairports` points, \>3000 African airports
6. `afripop2020` raster grid, population density 2020 from [WorldPop](https://www.worldpop.org/) aggregated to 20km squares
7. `afripop2000` raster grid, population density 2000 from [WorldPop](https://www.worldpop.org/) aggregated to 20km squares
8. `afrilandcover` raster grid, landcover in 2019, categorical, 20km from [MODIS](https://lpdaac.usgs.gov/products/mcd12c1v006/)


Lazy loading means that the objects should be accessible once `[library(afrilearndata)](https://rdrr.io/r/base/library.html)` is used.


If they are not recognised you can use e.g. `[data(africountries)](https://rdrr.io/r/utils/data.html)` to make sure the objects are loaded.


As well as providing the data as R objects the package provides them as files that can be used to demonstrate the process of reading spatial data into R and the read code is provided in the documentation of each dataset. The different datasets cover the following formats commonly used to store sptial data : geopackage, shapefile, kml, tiff, csv and grd.


Firstly, here are most of the data shown together. The `tmap` code to create this plot is shown later in the readme.


![](opensource/tidytuesday/2021-11-09/images/0.png)


Now looking at the data layers individually plotted with packages `sf` or `raster`



```


[library](https://rdrr.io/r/base/library.html)(afrilearndata)
[library](https://rdrr.io/r/base/library.html)([sf](https://r-spatial.github.io/sf/))

# polygons
[plot](https://r-spatial.github.io/sf/reference/plot.html)(sf::[st_geometry](https://r-spatial.github.io/sf/reference/st_geometry.html)(africountries))
```



```


# lines
[plot](https://r-spatial.github.io/sf/reference/plot.html)(sf::[st_geometry](https://r-spatial.github.io/sf/reference/st_geometry.html)(afrihighway))
```



```


# points
[plot](https://r-spatial.github.io/sf/reference/plot.html)(sf::[st_geometry](https://r-spatial.github.io/sf/reference/st_geometry.html)(africapitals))
```

![](opensource/tidytuesday/2021-11-09/images/1.png)


Population density data are from WorldPop clipped to Africa and aggregated to 20km resolution to make them more manageable. [WorldPop](https://www.worldpop.org/) datasets are licensed under [Creative Commons Attribution 4\.0 International](https://creativecommons.org/licenses/by/4.0/).



```


# raster grid
# install.packages("raster") # if not already installed
[library](https://rdrr.io/r/base/library.html)([raster](https://rspatial.org/raster))
[plot](https://rdrr.io/pkg/raster/man/plot.html)(afripop2020)
```

![](opensource/tidytuesday/2021-11-09/images/2.png)


The `africountries` data has country names in French, Portuguese, Swahili, Afrikaans and English, that can be used to label maps as follows.



```


[library](https://rdrr.io/r/base/library.html)(afrilearndata)

# install.packages("tmap") # if not already installed
[library](https://rdrr.io/r/base/library.html)([tmap](https://github.com/mtennekes/tmap))

[tm_shape](https://rdrr.io/pkg/tmap/man/tm_shape.html)(africountries) +
     [tm_borders](https://rdrr.io/pkg/tmap/man/tm_polygons.html)("grey", lwd = .5) +
     [tm_text](https://rdrr.io/pkg/tmap/man/tm_text.html)("name_fr", auto.placement=FALSE, remove.overlap=FALSE, just='centre', col='red4', size=0.7 )
```


Interactive maps can be created using the `mapview` package.



```


# install.packages("mapview") # if not already installed

[library](https://rdrr.io/r/base/library.html)([mapview](https://github.com/r-spatial/mapview))
mapview::[mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(africountries, zcol="name")
#here to show all airports on the continent
[mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(afriairports, zcol='type', label='name', cex=2)
  
```

Landcover data for the continent is provided as the majority landcover in 2019 at 20km resolution obtained from [MODIS](https://lpdaac.usgs.gov/products/mcd12c1v006/). An interactive landcover map can be displayed with `mapview`.



```


# install.packages("mapview") # if not already installed

[library](https://rdrr.io/r/base/library.html)([mapview](https://github.com/r-spatial/mapview))

[mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(afrilandcover,
       att="landcover",
       col.regions=[levels](https://rdrr.io/pkg/raster/man/factor.html)(afrilandcover)[[1]]$colour)
  
```

Here is a repeat of the map shown at the start of the readme, together with the code used to create it.



```


[library](https://rdrr.io/r/base/library.html)(afrilearndata)

# install.packages("tmap") # if not already installed
[library](https://rdrr.io/r/base/library.html)([tmap](https://github.com/mtennekes/tmap))

# tmap_mode("view") to set to tmap interactive viewing mode

[tm_shape](https://rdrr.io/pkg/tmap/man/tm_shape.html)(afripop2020) +
    [tm_raster](https://rdrr.io/pkg/tmap/man/tm_raster.html)(palette = [rev](https://rdrr.io/r/base/rev.html)(viridisLite::[magma](https://sjmgarnier.github.io/viridisLite/reference/viridis.html)(5)), breaks=[c](https://rdrr.io/r/base/c.html)(0,2,20,200,2000,25000)) +
[tm_shape](https://rdrr.io/pkg/tmap/man/tm_shape.html)(africountries) +
    [tm_borders](https://rdrr.io/pkg/tmap/man/tm_polygons.html)("white", lwd = .5) +
[tm_shape](https://rdrr.io/pkg/tmap/man/tm_shape.html)(afrihighway) +
    [tm_lines](https://rdrr.io/pkg/tmap/man/tm_lines.html)(col = "red") + 
[tm_shape](https://rdrr.io/pkg/tmap/man/tm_shape.html)(africapitals) +
    [tm_symbols](https://rdrr.io/pkg/tmap/man/tm_symbols.html)(col = "blue", alpha=0.4, scale = .6 )+
[tm_legend](https://rdrr.io/pkg/tmap/man/tm_layout.html)(show = FALSE)
```

![](opensource/tidytuesday/2021-11-09/images/3.png)




Learning Resources
------------------


For learning resources using these data see our [afrilearnr interactive tutorials](https://github.com/afrimapr/afrilearnr), resources in English \& French for a [4 hour entry level tutorial](https://github.com/afrimapr/r-maps-tutorial-fr-eng) and the in\-progress [afrimapr book](https://github.com/afrimapr/afrimapr-book).




Related
-------


For other and larger spatial datasets see the [spData package](https://github.com/Nowosad/spData) which was part of the inspiration for afrilearndata.




Contributions
-------------


afrilearndata is part of [afrimapr](https://afrimapr.github.io/afrimapr.website/) we welcome [issues and enhancement requests](https://github.com/afrimapr/afrilearndata/issues).







License
-------


* CC0




Developers
----------


* Andy South   
 Author, maintainer
* [All authors...](authors.html)






Developed by Andy South.




Site built with [pkgdown](https://pkgdown.r-lib.org/) 1\.6\.1\.








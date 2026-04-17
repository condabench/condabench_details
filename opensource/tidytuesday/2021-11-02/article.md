




Chapter 9 Making maps with R \| Geocomputation with R




































[Skip to main content](#content)

[Geocomputation with R](/)
--------------------------


Show table of contents





Table of contents
-----------------


* [Welcome](/)
* [Foreword (1st Edition)](/foreword-1st-edition)
* [Foreword (2nd Edition)](/foreword-2nd-edition)
* [Preface](/preface)
* [1 Introduction](/intro)
* Foundations
* [2 Geographic data in R](/spatial-class)
* [3 Attribute data operations](/attr)
* [4 Spatial data operations](/spatial-operations)
* [5 Geometry operations](/geometry-operations)
* [6 Raster\-vector interactions](/raster-vector)
* [7 Reprojecting geographic data](/reproj-geo-data)
* [8 Geographic data I/O](/read-write)
* Extensions
* [9 Making maps with R](/adv-map)
* [10 Bridges to GIS software](/gis)
* [11 Scripts, algorithms and functions](/algorithms)
* [12 Statistical learning](/spatial-cv)
* Applications
* [13 Transportation](/transport)
* [14 Geomarketing](/location)
* [15 Ecology](/eco)
* [16 Conclusion](/conclusion)
* [References](/references)



[View book source](https://github.com/geocompx/geocompr) 






9 Making maps with R
====================



Prerequisites
-------------


* This chapter requires the following packages that we have already been using:



```

[library](https://rdrr.io/r/base/library.html)([sf](https://r-spatial.github.io/sf/))
[library](https://rdrr.io/r/base/library.html)([terra](https://rspatial.org/))
[library](https://rdrr.io/r/base/library.html)([dplyr](https://dplyr.tidyverse.org))
[library](https://rdrr.io/r/base/library.html)([spData](https://jakubnowosad.com/spData/))
[library](https://rdrr.io/r/base/library.html)([spDataLarge](https://github.com/Nowosad/spData))
```

* The main package used in this chapter is **tmap**.
We recommend you to install its development version from the [r\-universe](https://r-universe.dev/) repository, which is updated more frequently than the CRAN version:



```

[install.packages](https://rdrr.io/r/utils/install.packages.html)("tmap", repos = [c](https://rdrr.io/r/base/c.html)("https://r-tmap.r-universe.dev",
                                   "https://cloud.r-project.org"))
```

* It uses the following visualization packages (also install **shiny** if you want to develop interactive mapping applications):



```

[library](https://rdrr.io/r/base/library.html)([tmap](https://github.com/r-tmap/tmap))    # for static and interactive maps
[library](https://rdrr.io/r/base/library.html)([leaflet](https://rstudio.github.io/leaflet/)) # for interactive maps
[library](https://rdrr.io/r/base/library.html)([ggplot2](https://ggplot2.tidyverse.org)) # tidyverse data visualization package
```

* You also need to read\-in a couple of datasets as follows for Section [4\.3](/spatial-operations#spatial-ras):



```

nz_elev = [rast](https://rspatial.github.io/terra/reference/rast.html)([system.file](https://rdrr.io/r/base/system.file.html)("raster/nz_elev.tif", package = "spDataLarge"))
```



9\.1 Introduction
-----------------


A satisfying and important aspect of geographic research is communicating the results.
Map\-making — the art of cartography — is an ancient skill involving communication, attention to detail, and an element of creativity.
Static mapping in R is straightforward with the `[plot()](https://rspatial.github.io/terra/reference/plot.html)` function, as we saw in Section [2\.2\.3](/spatial-class#basic-map).
It is possible to create advanced maps using base R methods ([Murrell 2016](/references#ref-murrell_r_2016)).
The focus of this chapter, however, is cartography with dedicated map\-making packages.
When learning a new skill, it makes sense to gain depth\-of\-knowledge in one area before branching out.
Map\-making is no exception, hence this chapter’s coverage of one package (**tmap**) in depth rather than many superficially.


In addition to being fun and creative, cartography also has important practical applications.
A carefully crafted map can be the best way of communicating the results of your work, but poorly designed maps can leave a bad impression.
Common design issues include poor placement, size and readability of text and careless selection of colors, as outlined in the [style guide](https://files.taylorandfrancis.com/TJOM-suppmaterial-quick-guide.pdf) of the *Journal of Maps*.
Furthermore, poor map\-making can hinder the communication of results ([Brewer 2015](/references#ref-brewer_designing_2015)):



> Amateur\-looking maps can undermine your audience’s ability to understand important information and weaken the presentation of a professional data investigation.
> Maps have been used for several thousand years for a wide variety of purposes.
> Historic examples include maps of buildings and land ownership in the Old Babylonian dynasty more than 3000 years ago and Ptolemy’s world map in his masterpiece *Geography* nearly 2000 years ago ([Talbert 2014](/references#ref-talbert_ancient_2014)).


Map\-making has historically been an activity undertaken only by, or on behalf of, the elite.
This has changed with the emergence of open source mapping software such as the R package **tmap** and the ‘print layout’ in QGIS, which allow anyone to make high\-quality maps, enabling ‘citizen science’.
Maps are also often the best way to present the findings of geocomputational research in a way that is accessible.
Map\-making is therefore a critical part of geocomputation and its emphasis is not only on describing, but also *changing* the world.


This chapter shows how to make a wide range of maps.
The next section covers a range of static maps, including aesthetic considerations, facets and inset maps.
Sections [9\.3](/adv-map#animated-maps) to [9\.5](/adv-map#mapping-applications) cover animated and interactive maps (including web maps and mapping applications).
Finally, Section [9\.6](/adv-map#other-mapping-packages) covers a range of alternative map\-making packages including **ggplot2** and **cartogram**.




9\.2 Static maps
----------------



Static maps are the most common type of visual output from geocomputation.
They are usually stored in standard formats including `.png` and `.pdf` for *graphical* raster and vector outputs, respectively.
Initially, static maps were the only type of maps that R could produce.
Things have advanced with the release of **sp** (see [Pebesma and Bivand 2005](/references#ref-pebesma_classes_2005)), and many map\-making techniques, functions, and packages have been developed since then.
However, despite the innovation of interactive mapping, static plotting was still the emphasis of geographic data visualization in R a decade later ([Cheshire and Lovelace 2015](/references#ref-cheshire_spatial_2015)).


The generic `[plot()](https://rspatial.github.io/terra/reference/plot.html)` function is often the fastest way to create static maps from vector and raster spatial objects (see Sections [2\.2\.3](/spatial-class#basic-map) and [2\.3\.3](/spatial-class#basic-map-raster)).
Sometimes, simplicity and speed are priorities, especially during the development phase of a project, and this is where `[plot()](https://rspatial.github.io/terra/reference/plot.html)` excels.
The base R approach is also extensible, with `[plot()](https://rspatial.github.io/terra/reference/plot.html)` offering dozens of arguments.
Another approach is the **grid** package which allows low\-level control of static maps, as illustrated in chapter [14](https://www.stat.auckland.ac.nz/~paul/RG2e/chapter14.html) of Murrell ([2016](/references#ref-murrell_r_2016)).
This part of the book focuses on **tmap** and emphasizes the essential aesthetic and layout options.



**tmap** is a powerful and flexible map\-making package with sensible defaults.
It has a concise syntax that allows for the creation of attractive maps with minimal code which will be familiar to **ggplot2** users.
It also has the unique capability to generate static and interactive maps using the same code via `[tmap_mode()](https://r-tmap.github.io/tmap/reference/tmap_mode.html)`.
Finally, it accepts a wider range of spatial classes (including **sf** and **terra** objects) than alternatives such as **ggplot2**.



### 9\.2\.1 tmap basics



Like **ggplot2**, **tmap** is based on the idea of a ‘grammar of graphics’ ([Wilkinson and Wills 2005](/references#ref-wilkinson_grammar_2005)).
This involves a separation between the input data and the aesthetics (how data are visualized): each input dataset can be ‘mapped’ in a range of different ways including location on the map (defined by data’s `geometry`), color, and other visual variables.
The basic building block is `[tm_shape()](https://r-tmap.github.io/tmap/reference/tm_shape.html)` (which defines input data: a vector or raster object), followed by one or more layer elements such as `[tm_fill()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` and `[tm_dots()](https://r-tmap.github.io/tmap/reference/tm_symbols.html)`.
This layering is demonstrated in the chunk below, which generates the maps presented in Figure [9\.1](/adv-map#fig:tmshape):



```

# Add fill layer to nz shape
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) +
  [tm_fill](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() 
# Add border layer to nz shape
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) +
  [tm_borders](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() 
# Add fill and border layers to nz shape
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) +
  [tm_fill](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() +
  [tm_borders](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() 
```




FIGURE 9\.1: New Zealand’s shape plotted with fill (left), border (middle) and fill and border (right) layers added using tmap functions.




The object passed to `[tm_shape()](https://r-tmap.github.io/tmap/reference/tm_shape.html)` in this case is `nz`, an `sf` object representing the regions of New Zealand (see Section [2\.2\.1](/spatial-class#intro-sf) for more on `sf` objects).
Layers are added to represent `nz` visually, with `[tm_fill()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` and `[tm_borders()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` creating shaded areas (left panel) and border outlines (middle panel) in Figure [9\.1](/adv-map#fig:tmshape), respectively.



This is an intuitive approach to map\-making:
the common task of *adding* new layers is undertaken by the addition operator `+`, followed by `tm_*()`.
The asterisk (\*) refers to a wide range of layer types which have self\-explanatory names including:


* `[tm_fill()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)`: shaded areas for (multi)polygons
* `[tm_borders()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)`: border outlines for (multi)polygons
* `[tm_polygons()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)`: both, shaded areas and border outlines for (multi)polygons
* `[tm_lines()](https://r-tmap.github.io/tmap/reference/tm_lines.html)`: lines for (multi)linestrings
* `[tm_symbols()](https://r-tmap.github.io/tmap/reference/tm_symbols.html)`: symbols for (multi)points, (multi)linestrings, and (multi)polygons
* `[tm_raster()](https://r-tmap.github.io/tmap/reference/tm_raster.html)`: colored cells of raster data (there is also `[tm_rgb()](https://r-tmap.github.io/tmap/reference/tm_rgb.html)` for rasters with three layers)
* `[tm_text()](https://r-tmap.github.io/tmap/reference/tm_text.html)`: text information for (multi)points, (multi)linestrings, and (multi)polygons


This layering is illustrated in the right panel of Figure [9\.1](/adv-map#fig:tmshape), the result of adding a border *on top of* the fill layer.



`[qtm()](https://r-tmap.github.io/tmap/reference/qtm.html)` is a handy function to create **q**uick **t**hematic **m**aps (hence the snappy name).
It is concise and provides a good default visualization in many cases:
`qtm(nz)`, for example, is equivalent to `tm_shape(nz) + tm_fill() + tm_borders()`.
Further, layers can be added concisely using multiple `[qtm()](https://r-tmap.github.io/tmap/reference/qtm.html)` calls, such as `qtm(nz) + qtm(nz_height)`.
The disadvantage is that it makes aesthetics of individual layers harder to control, explaining why we avoid teaching it in this chapter.



### 9\.2\.2 Map objects


A useful feature of **tmap** is its ability to store *objects* representing maps.
The code chunk below demonstrates this by saving the last plot in Figure [9\.1](/adv-map#fig:tmshape) as an object of class `tmap` (note the use of `[tm_polygons()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` which condenses `tm_fill() + tm_borders()` into a single function):



```

map_nz = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)()
[class](https://rdrr.io/r/base/class.html)(map_nz)
#> [1] "tmap"
```

`map_nz` can be plotted later, for example by adding other layers (as shown below) or simply running `map_nz` in the console, which is equivalent to `print(map_nz)`.


New *shapes* can be added with `+ tm_shape(new_obj)`.
In this case, `new_obj` represents a new spatial object to be plotted on top of preceding layers.
When a new shape is added in this way, all subsequent aesthetic functions refer to it, until another new shape is added.
This syntax allows the creation of maps with multiple shapes and layers, as illustrated in the next code chunk which uses the function `[tm_raster()](https://r-tmap.github.io/tmap/reference/tm_raster.html)` to plot a raster layer (with `col_alpha` set to make the layer semi\-transparent):



```

map_nz1 = map_nz +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_elev) + [tm_raster](https://r-tmap.github.io/tmap/reference/tm_raster.html)(col_alpha = 0.7)
```

Building on the previously created `map_nz` object, the preceding code creates a new map object `map_nz1` that contains another shape (`nz_elev`) representing average elevation across New Zealand (see Figure [9\.2](/adv-map#fig:tmlayers), left).
More shapes and layers can be added, as illustrated in the code chunk below which creates `nz_water`, representing New Zealand’s [territorial waters](https://en.wikipedia.org/wiki/Territorial_waters), and adds the resulting lines to an existing map object.



```

nz_water = [st_union](https://r-spatial.github.io/sf/reference/geos_combine.html)(nz) |>
  [st_buffer](https://r-spatial.github.io/sf/reference/geos_unary.html)(22200) |> 
  [st_cast](https://r-spatial.github.io/sf/reference/st_cast.html)(to = "LINESTRING")
map_nz2 = map_nz1 +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_water) + [tm_lines](https://r-tmap.github.io/tmap/reference/tm_lines.html)()
```

There is no limit to the number of layers or shapes that can be added to `tmap` objects, and the same shape can even be used multiple times.
The final map illustrated in Figure [9\.2](/adv-map#fig:tmlayers) is created by adding a layer representing high points (stored in the object `nz_height`) onto the previously created `map_nz2` object with `[tm_symbols()](https://r-tmap.github.io/tmap/reference/tm_symbols.html)` (see `[?tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)` for details on **tmap**’s point plotting functions).
The resulting map, which has four layers, is illustrated in the right\-hand panel of Figure [9\.2](/adv-map#fig:tmlayers):



```

map_nz3 = map_nz2 +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_height) + [tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)()
```


A useful and little known feature of **tmap** is that multiple map objects can be arranged in a single ‘metaplot’ with `[tmap_arrange()](https://r-tmap.github.io/tmap/reference/tmap_arrange.html)`.
This is demonstrated in the code chunk below which plots `map_nz1` to `map_nz3`, resulting in Figure [9\.2](/adv-map#fig:tmlayers).



```

[tmap_arrange](https://r-tmap.github.io/tmap/reference/tmap_arrange.html)(map_nz1, map_nz2, map_nz3)
```




FIGURE 9\.2: Maps with added layers to the final map of Figure 9\.1\.




More elements can also be added with the `+` operator.
Aesthetic settings, however, are controlled by arguments to layer functions.




### 9\.2\.3 Visual variables



The plots in the previous section demonstrate **tmap**’s default aesthetic settings.
Gray shades are used for `[tm_fill()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` and `[tm_symbols()](https://r-tmap.github.io/tmap/reference/tm_symbols.html)` layers and a continuous black line is used to represent lines created with `[tm_lines()](https://r-tmap.github.io/tmap/reference/tm_lines.html)`.
Of course, these default values and other aesthetics can be overridden.
The purpose of this section is to show how.


There are two main types of map aesthetics: those that change with the data and those that are constant.
Unlike **ggplot2**, which uses the helper function `[aes()](https://ggplot2.tidyverse.org/reference/aes.html)` to represent variable aesthetics, **tmap** accepts a few aesthetic arguments, depending on a selected layer type:


* `fill`: fill color of a polygon
* `col`: color of a polygon border, line, point, or raster
* `lwd`: line width
* `lty`: line type
* `size`: size of a symbol
* `shape`: shape of a symbol


Additionally, we may customize the fill and border color transparency using `fill_alpha` and `col_alpha`.


To map a variable to an aesthetic, pass its column name to the corresponding argument, and to set a fixed aesthetic, pass the desired value instead.48
The impact of setting these with fixed values is illustrated in Figure [9\.3](/adv-map#fig:tmstatic).



```

ma1 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "red")
ma2 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "red", fill_alpha = 0.3)
ma3 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(col = "blue")
ma4 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(lwd = 3)
ma5 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(lty = 2)
ma6 = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "red", fill_alpha = 0.3,
                                 col = "blue", lwd = 3, lty = 2)
[tmap_arrange](https://r-tmap.github.io/tmap/reference/tmap_arrange.html)(ma1, ma2, ma3, ma4, ma5, ma6)
```




FIGURE 9\.3: Impact of changing commonly used fill and border aesthetics to fixed values.




Like base R plots, arguments defining aesthetics can also receive values that vary.
Unlike the base R code below (which generates the left panel in Figure [9\.4](/adv-map#fig:tmcol)), **tmap** aesthetic arguments will not accept a numeric vector:



```

[plot](https://rspatial.github.io/terra/reference/plot.html)([st_geometry](https://r-spatial.github.io/sf/reference/st_geometry.html)(nz), col = nz$Land_area)  # works
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_fill](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = nz$Land_area) # fails
#> Error: palette should be a character value
```

Instead `fill` (and other aesthetics that can vary such as `lwd` for line layers and `size` for point layers) requires a character string naming an attribute associated with the geometry to be plotted.
Thus, one would achieve the desired result as follows (Figure [9\.4](/adv-map#fig:tmcol), right panel):



```

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_fill](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Land_area")
```




FIGURE 9\.4: Comparison of base (left) and tmap (right) handling of a numeric color field.




Each visual variable has three related additional arguments, with suffixes of `.scale`, `.legend`, and `.free`.
For example, the `[tm_fill()](https://r-tmap.github.io/tmap/reference/tm_polygons.html)` function has arguments such as `fill`, `fill.scale`, `fill.legend`, and `fill.free`.
The `.scale` argument determines how the provided values are represented on the map and in the legend (Section [9\.2\.4](/adv-map#scales)), while the `.legend` argument is used to customize the legend settings, such as its title, orientation, or position (Section [9\.2\.5](/adv-map#legends)).
The `.free` argument is relevant only for maps with many facets to determine if each facet has the same or different scale and legend.




### 9\.2\.4 Scales



Scales control how the values are represented on the map and in the legend, and they largely depend on the selected visual variable.
For example, when our visual variable is `col`, then `col.scale` controls how the colors of spatial objects are related to the provided values; and when our visual variable is `size`, then `size.scale` controls how the sizes represent the provided values.
By default, the used scale is `[tm_scale()](https://r-tmap.github.io/tmap/reference/tm_scale.html)`, which selects the visual settings automatically given by the input data type (factor, numeric, and integer).



Let’s see how the scales work by customizing polygons’ fill colors.
Color settings are an important part of map design – they can have a major impact on how spatial variability is portrayed as illustrated in Figure [9\.5](/adv-map#fig:tmpal).
This figure shows four ways of coloring regions in New Zealand depending on median income, from left to right (and demonstrated in the code chunk below):


* The default setting uses ‘pretty’ breaks, described in the next paragraph
* `breaks` allows you to manually set the breaks
* `n` sets the number of bins into which numeric variables are categorized
* `values` defines the color scheme, for example, `BuGn`



```

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Median_income")
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Median_income",
                        fill.scale = [tm_scale](https://r-tmap.github.io/tmap/reference/tm_scale.html)(breaks = [c](https://rdrr.io/r/base/c.html)(0, 30000, 40000, 50000)))
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Median_income",
                           fill.scale = [tm_scale](https://r-tmap.github.io/tmap/reference/tm_scale.html)(n = 10))
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Median_income",
                           fill.scale = [tm_scale](https://r-tmap.github.io/tmap/reference/tm_scale.html)(values = "BuGn"))
```




FIGURE 9\.5: Color settings. The results show (from left to right): default settings, manual breaks, n breaks, and the impact of changing the palette.





All of the above arguments (`breaks`, `n`, and `values`) also work for other types of visual variables.
For example, `values` expects a vector of colors or a palette name for `fill.scale` or `col.scale`, a vector of sizes for `size.scale`, or a vector of symbols for `shape.scale`.


We are also able to customize scales using a family of functions that start with the `tm_scale_` prefix.
The most important ones are `[tm_scale_intervals()](https://r-tmap.github.io/tmap/reference/tm_scale_intervals.html)`, `[tm_scale_continuous()](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)`, and `[tm_scale_categorical()](https://r-tmap.github.io/tmap/reference/tm_scale_categorical.html)`.



The `[tm_scale_intervals()](https://r-tmap.github.io/tmap/reference/tm_scale_intervals.html)` function splits the input data values into a set of intervals.
In addition to manually setting `breaks`, **tmap** allows users to specify algorithms to create breaks with the `style` argument automatically.
The default is `tm_scale_intervals(style = "pretty")`, which rounds breaks into whole numbers where possible and spaces them evenly.
Other options are listed below and presented in Figure [9\.6](/adv-map#fig:break-styles).


* `style = "equal"`: divides input values into bins of equal range and is appropriate for variables with a uniform distribution (not recommended for variables with a skewed distribution as the resulting map may end up having little color diversity)
* `style = "quantile"`: ensures the same number of observations fall into each category (with the potential downside that bin ranges can vary widely)
* `style = "jenks"`: identifies groups of similar values in the data and maximizes the differences between categories
* `style = "log10_pretty"`: a common logarithmic (the logarithm to base 10\) version of the regular pretty style used for variables with a right\-skewed distribution



Although `style` is an argument of **tmap** functions, in fact it originates as an argument in `[classInt::classIntervals()](https://r-spatial.github.io/classInt/reference/classIntervals.html)` — see the help page of this function for details.




FIGURE 9\.6: Different interval scale methods set using the style argument in tmap.





The `[tm_scale_continuous()](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)` function presents a continuous color field and is particularly suited for continuous rasters (Figure [9\.7](/adv-map#fig:concat), left panel).
In case of variables with q skewed distribution, you can also use its variants – `[tm_scale_continuous_log()](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)` and `[tm_scale_continuous_log1p()](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)`.
Finally, `[tm_scale_categorical()](https://r-tmap.github.io/tmap/reference/tm_scale_categorical.html)` was designed to represent categorical values and ensures that each category receives a unique color (Figure [9\.7](/adv-map#fig:concat), right panel).





FIGURE 9\.7: Continuous and categorical scales in tmap.





Palettes define the color ranges associated with the bins and determined by the `tm_scale_*()` functions, and its `breaks` and `n` arguments described above.
It expects a vector of colors or a new color palette name, which can be found interactively with `[cols4all::c4a_gui()](https://mtennekes.github.io/cols4all/reference/c4a_gui.html)`.
You can also add a `-` as the color palette name prefix to reverse the palette order.



All of the default `values` of the visual variables, such as default color palettes for different types of input variables, can be found with `[tmap_options()](https://r-tmap.github.io/tmap/reference/tmap_options.html)`.
For example, run `tmap_options()$values.var`.


There are three main groups of color palettes: categorical, sequential and diverging (Figure [9\.8](/adv-map#fig:colpal)), and each of them serves a different purpose.49
Categorical palettes consist of easily distinguishable colors and are most appropriate for categorical data without any particular order such as state names or land cover classes.
Colors should be intuitive: rivers should be blue, for example, and pastures green.
Avoid too many categories: maps with large legends and many colors can be uninterpretable.50


The second group is sequential palettes.
These follow a gradient, for example from light to dark colors (light colors often tend to represent lower values), and are appropriate for continuous (numeric) variables.
Sequential palettes can be single (`greens` goes from light to dark green, for example) or multi\-color/hue (`yl_gn_bu` is gradient from light yellow to blue via green, for example), as demonstrated in the code chunk below — output not shown, run the code yourself to see the results!



```

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + 
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)("Median_income", fill.scale = [tm_scale](https://r-tmap.github.io/tmap/reference/tm_scale.html)(values = "greens"))
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + 
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)("Median_income", fill.scale = [tm_scale](https://r-tmap.github.io/tmap/reference/tm_scale.html)(values = "yl_gn_bu"))
```

The third group, diverging palettes, typically range between three distinct colors (purple\-white\-green in Figure [9\.8](/adv-map#fig:colpal)) and are usually created by joining two single\-color sequential palettes with the darker colors at each end.
Their main purpose is to visualize the difference from an important reference point, e.g., a certain temperature, the median household income or the mean probability for a drought event.
The reference point’s value can be adjusted in **tmap** using the `midpoint` argument.



```

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + 
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)("Median_income",
              fill.scale = [tm_scale_continuous](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)(values = "pu_gn_div", 
                                               midpoint = 28000))
```




FIGURE 9\.8: Examples of categorical, sequential and diverging palettes.




There are two important principles for consideration when working with colors: perceptibility and accessibility.
Firstly, colors on maps should match our perception.
This means that certain colors are viewed through our experience and also cultural lenses.
For example, green colors usually represent vegetation or lowlands, and blue is connected with water or coolness.
Color palettes should also be easy to understand to effectively convey information.
It should be clear which values are lower and which are higher, and colors should change gradually.
Secondly, changes in colors should be accessible to the largest number of people.
Therefore, it is important to use colorblind friendly palettes as often as possible.51




### 9\.2\.5 Legends



After we decided on our visual variable and its properties, we should move our attention toward the related map legend style.
Using the `[tm_legend()](https://r-tmap.github.io/tmap/reference/tm_legend.html)` function, we may change its title, position, orientation, or even disable it.
The most important argument in this function is `title`, which sets the title of the associated legend.
In general, a map legend title should provide two pieces of information: what the legend represents and what the units are of the presented variable.
The following code chunk demonstrates this functionality by providing a more attractive name than the variable name `Land_area` (note the use of `[expression()](https://rdrr.io/r/base/expression.html)` to create superscript text):



```

legend_title = [expression](https://rdrr.io/r/base/expression.html)("Area (km"^2*")")
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) +
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Land_area", fill.legend = [tm_legend](https://r-tmap.github.io/tmap/reference/tm_legend.html)(title = legend_title))
```

The default legend orientation in **tmap** is `"portrait"`, however, an alternative legend orientation, `"landscape"`, is also possible.
Other than that, we can also customize the location of the legend using the `position` argument.



```

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) +
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(fill = "Land_area",
              fill.legend = [tm_legend](https://r-tmap.github.io/tmap/reference/tm_legend.html)(title = legend_title,
                                      orientation = "landscape",
                                      position = [tm_pos_out](https://r-tmap.github.io/tmap/reference/tm_pos.html)("center", "bottom")))
```

The legend position (and also the position of several other map elements in **tmap**) can be customized using one of a few functions.
The two most important are:


* `[tm_pos_out()](https://r-tmap.github.io/tmap/reference/tm_pos.html)`: the default, adds the legend outside of the map frame area.
We can customize its location with two values that represent the horizontal position (`"left"`, `"center"`, or `"right"`), and the vertical position (`"bottom"`, `"center"`, or `"top"`)
* `[tm_pos_in()](https://r-tmap.github.io/tmap/reference/tm_pos.html)`: puts the legend inside of the map frame area.
We may decide on its position using two arguments, where the first one can be `"left"`, `"center"`, or `"right"`, and the second one can be `"bottom"`, `"center"`, or `"top"`.


Alternatively, we may just provide a vector of two values (or two numbers between 0 and 1\) here – and in such case, the legend will be put inside the map frame.




### 9\.2\.6 Layouts



The map layout refers to the combination of all map elements into a cohesive map.
Map elements include among others the objects to be mapped, the map grid, the scale bar, the title, and margins, while the color settings covered in the previous section relate to the palette and breakpoints used to affect how the map looks.
Both may result in subtle changes that can have an equally large impact on the impression left by your maps.


Additional map elements such as graticules , north arrows, scale bars and map titles have their own functions: `[tm_graticules()](https://r-tmap.github.io/tmap/reference/tm_graticules.html)`, `[tm_compass()](https://r-tmap.github.io/tmap/reference/tm_compass.html)`, `[tm_scalebar()](https://r-tmap.github.io/tmap/reference/tm_scalebar.html)`, and `[tm_title()](https://r-tmap.github.io/tmap/reference/tm_title.html)` (Figure [9\.9](/adv-map#fig:na-sb)).52



```

map_nz + 
  [tm_graticules](https://r-tmap.github.io/tmap/reference/tm_graticules.html)() +
  [tm_compass](https://r-tmap.github.io/tmap/reference/tm_compass.html)(type = "8star", position = [c](https://rdrr.io/r/base/c.html)("left", "top")) +
  [tm_scalebar](https://r-tmap.github.io/tmap/reference/tm_scalebar.html)(breaks = [c](https://rdrr.io/r/base/c.html)(0, 100, 200), text.size = 1, position = [c](https://rdrr.io/r/base/c.html)("left", "top")) +
  [tm_title](https://r-tmap.github.io/tmap/reference/tm_title.html)("New Zealand")
```




FIGURE 9\.9: Map with additional elements: a north arrow and scale bar.




**tmap** also allows a wide variety of layout settings to be changed, some of which, produced using the following code (see `args(tm_layout)` or `[?tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)` for a full list), are illustrated in Figure [9\.10](/adv-map#fig:layout1).



```

map_nz + [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(scale = 4)
map_nz + [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(bg.color = "lightblue")
map_nz + [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(frame = FALSE)
```




FIGURE 9\.10: Layout options specified by (from left to right) scale, bg.color, and frame arguments.




The other arguments in `[tm_layout()](https://r-tmap.github.io/tmap/reference/tm_layout.html)` provide control over many more aspects of the map in relation to the canvas on which it is placed.
Here are some useful layout settings (some of which are illustrated in Figure [9\.11](/adv-map#fig:layout2)):


* Margin settings including `inner.margin` and `outer.margin`
* Font settings controlled by `fontface` and `fontfamily`
* Legend settings including options such as `legend.show` (whether or not to show the legend) `legend.orientation`, `legend.position`, and `legend.frame`
* Frame width (`frame.lwd`) and an option to allow double lines (`frame.double.line`)
* Color settings controlling `color.sepia.intensity` (how *yellowy* the map looks) and `color.saturation` (a color\-grayscale)





FIGURE 9\.11: Selected layout options.






### 9\.2\.7 Faceted maps



Faceted maps, also referred to as ‘small multiples’, are composed of many maps arranged side\-by\-side, and sometimes stacked vertically ([Meulemans et al. 2017](/references#ref-meulemans_small_2017)).
Facets enable the visualization of how spatial relationships change with respect to another variable, such as time.
The changing populations of settlements, for example, can be represented in a faceted map with each panel representing the population at a particular moment in time.
The time dimension could be represented via another *visual variable* such as color.
However, this risks cluttering the map because it will involve multiple overlapping points (cities do not tend to move over time!).


Typically all individual facets in a faceted map contain the same geometry data repeated multiple times, once for each column in the attribute data (this is the default plotting method for `sf` objects, see Chapter [2](/spatial-class#spatial-class)).
However, facets can also represent shifting geometries such as the evolution of a point pattern over time.
This use case of a faceted plot is illustrated in Figure [9\.12](/adv-map#fig:urban-facet).



```

urb_1970_2030 = urban_agglomerations |> 
  [filter](https://dplyr.tidyverse.org/reference/filter.html)(year [%in%](https://rspatial.github.io/terra/reference/match.html) [c](https://rdrr.io/r/base/c.html)(1970, 1990, 2010, 2030))

[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(world) +
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(urb_1970_2030) +
  [tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)(fill = "black", col = "white", size = "population_millions") +
  [tm_facets_wrap](https://r-tmap.github.io/tmap/reference/tm_facets.html)(by = "year", nrow = 2)
```




FIGURE 9\.12: Faceted map showing the top 30 largest urban agglomerations from 1970 to 2030 based on population projections by the United Nations.




The preceding code chunk demonstrates key features of faceted maps created using the `[tm_facets_wrap()](https://r-tmap.github.io/tmap/reference/tm_facets.html)` function:


* Shapes that do not have a facet variable are repeated (countries in `world` in this case)
* The `by` argument which varies depending on a variable (`"year"` in this case)
* The `nrow`/`ncol` setting specifying the number of rows and columns that facets should be arranged into


Alternatively, it is possible to use the `[tm_facets_grid()](https://r-tmap.github.io/tmap/reference/tm_facets.html)` function that allows to have facets based on up to three different variables: one for `rows`, one for `columns`, and possibly one for `pages`.


In addition to their utility for showing changing spatial relationships, faceted maps are also useful as the foundation for animated maps (see Section [9\.3](/adv-map#animated-maps)).




### 9\.2\.8 Inset maps



An inset map is a smaller map rendered within or next to the main map.
It could serve many different purposes, including providing a context (Figure [9\.13](/adv-map#fig:insetmap1)) or bringing some non\-contiguous regions closer to ease their comparison (Figure [9\.14](/adv-map#fig:insetmap2)).
They could be also used to focus on a smaller area in more detail or to cover the same area as the map, but representing a different topic.


In the example below, we create a map of the central part of New Zealand’s Southern Alps.
Our inset map will show where the main map is in relation to the whole New Zealand.
The first step is to define the area of interest, which can be done by creating a new spatial object, `nz_region`.



```

nz_region = [st_bbox](https://r-spatial.github.io/sf/reference/st_bbox.html)([c](https://rdrr.io/r/base/c.html)(xmin = 1340000, xmax = 1450000,
                      ymin = 5130000, ymax = 5210000),
                    crs = [st_crs](https://r-spatial.github.io/sf/reference/st_crs.html)(nz_height)) |> 
  [st_as_sfc](https://r-spatial.github.io/sf/reference/st_as_sfc.html)()
```

In the second step, we create a base\-map showing New Zealand’s Southern Alps area.
This is a place where the most important message is stated.



```

nz_height_map = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_elev, bbox = nz_region) +
  [tm_raster](https://r-tmap.github.io/tmap/reference/tm_raster.html)(col.scale = [tm_scale_continuous](https://r-tmap.github.io/tmap/reference/tm_scale_continuous.html)(values = "YlGn"),
            col.legend = [tm_legend](https://r-tmap.github.io/tmap/reference/tm_legend.html)(position = [c](https://rdrr.io/r/base/c.html)("left", "top"))) +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_height) + [tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)(shape = 2, col = "red", size = 1) +
  [tm_scalebar](https://r-tmap.github.io/tmap/reference/tm_scalebar.html)(position = [c](https://rdrr.io/r/base/c.html)("left", "bottom"))
```

The third step consists of the inset map creation.
It gives a context and helps to locate the area of interest.
Importantly, this map needs to clearly indicate the location of the main map, for example by stating its borders.



```

nz_map = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() +
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_height) + [tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)(shape = 2, col = "red", size = 0.1) + 
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_region) + [tm_borders](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(lwd = 3) +
  [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(bg.color = "lightblue")
```

One of the main differences between regular charts (e.g., scatterplots) and maps is that the input data determine the aspect ratio of maps.
Thus, in this case, we need to calculate the aspect ratios of our two main datasets, `nz_region` and `nz`.
The following function, `norm_dim()` returns the normalized width (`"w"`) and height (`"h"`) of the object (as `"snpc"` units understood by the graphic device).



```

[library](https://rdrr.io/r/base/library.html)(grid)
norm_dim = function(obj){
    bbox = [st_bbox](https://r-spatial.github.io/sf/reference/st_bbox.html)(obj)
    width = bbox[["xmax"]] - bbox[["xmin"]]
    height = bbox[["ymax"]] - bbox[["ymin"]]
    w = width / [max](https://rdrr.io/r/base/Extremes.html)(width, height)
    h = height / [max](https://rdrr.io/r/base/Extremes.html)(width, height)
    [return](https://rdrr.io/r/base/function.html)([unit](https://rdrr.io/r/grid/unit.html)([c](https://rdrr.io/r/base/c.html)(w, h), "snpc"))
}
main_dim = norm_dim(nz_region)
ins_dim = norm_dim(nz)
```

Next, knowing the aspect ratios, we need to specify the sizes and locations of our two maps – the main map and the inset map – using the `[viewport()](https://rdrr.io/r/grid/viewport.html)` function.
A viewport is part of a graphics device we use to draw the graphical elements at a given moment.
The viewport of our main map is just the representation of its aspect ratio.



```

main_vp = [viewport](https://rdrr.io/r/grid/viewport.html)(width = main_dim[1], height = main_dim[2])
```

On the other hand, the viewport of the inset map needs to specify its size and location.
Here, we would make the inset map twice smaller as the main one by multiplying the width and height by 0\.5, and we will locate it 0\.5 cm from the bottom right of the main map frame.



```

ins_vp = [viewport](https://rdrr.io/r/grid/viewport.html)(width = ins_dim[1] * 0.5, height = ins_dim[2] * 0.5,
                  x = [unit](https://rdrr.io/r/grid/unit.html)(1, "npc") - [unit](https://rdrr.io/r/grid/unit.html)(0.5, "cm"), y = [unit](https://rdrr.io/r/grid/unit.html)(0.5, "cm"),
                  just = [c](https://rdrr.io/r/base/c.html)("right", "bottom"))
```

Finally, we combine the two maps by creating a new, blank canvas, printing out the main map, and then placing the inset map inside of the main map viewport.



```

[grid.newpage](https://rdrr.io/r/grid/grid.newpage.html)()
[print](https://rdrr.io/r/base/print.html)(nz_height_map, vp = main_vp)
[pushViewport](https://rdrr.io/r/grid/viewports.html)(main_vp)
[print](https://rdrr.io/r/base/print.html)(nz_map, vp = ins_vp)
```




FIGURE 9\.13: Inset map providing a context – location of the central part of the Southern Alps in New Zealand.




Inset maps can be saved to file either by using a graphic device (see Section [8\.9](/read-write#visual-outputs)) or the `[tmap_save()](https://r-tmap.github.io/tmap/reference/tmap_save.html)` function and its arguments: `insets_tm` and `insets_vp`.


Inset maps are also used to create one map of non\-contiguous areas.
Probably, the most often used example is a map of the United States, which consists of the contiguous United States, Hawaii and Alaska.
It is very important to find the best projection for each individual inset in these types of cases (see Chapter [7](/reproj-geo-data#reproj-geo-data) to learn more).
We can use US National Atlas Equal Area for the map of the contiguous United States by putting its EPSG code in the `crs` argument of `[tm_shape()](https://r-tmap.github.io/tmap/reference/tm_shape.html)`.



```

us_states_map = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(us_states, crs = "EPSG:9311") + 
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() + 
  [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(frame = FALSE)
```

The rest of our objects, `hawaii` and `alaska`, already have proper projections; therefore, we just need to create two separate maps:



```

hawaii_map = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(hawaii) +
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() + 
  [tm_title](https://r-tmap.github.io/tmap/reference/tm_title.html)("Hawaii") +
  [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(frame = FALSE, bg.color = NA, 
            title.position = [c](https://rdrr.io/r/base/c.html)("LEFT", "BOTTOM"))
alaska_map = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(alaska) +
  [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() + 
  [tm_title](https://r-tmap.github.io/tmap/reference/tm_title.html)("Alaska") +
  [tm_layout](https://r-tmap.github.io/tmap/reference/tm_layout.html)(frame = FALSE, bg.color = NA)
```

The final map is created by combining, resizing and arranging these three maps:



```

us_states_map
[print](https://rdrr.io/r/base/print.html)(hawaii_map, vp = grid::[viewport](https://rdrr.io/r/grid/viewport.html)(0.35, 0.1, width = 0.2, height = 0.1))
[print](https://rdrr.io/r/base/print.html)(alaska_map, vp = grid::[viewport](https://rdrr.io/r/grid/viewport.html)(0.15, 0.15, width = 0.3, height = 0.3))
```




FIGURE 9\.14: Map of the United States.




The code presented above is compact and can be used as the basis for other inset maps, but the results, in Figure [9\.14](/adv-map#fig:insetmap2), provide a poor representation of the locations and sizes of Hawaii and Alaska.
For a more in\-depth approach, see the [`us-map`](https://geocompx.github.io/geocompkg/articles/us-map.html) vignette from the **geocompkg**.





9\.3 Animated maps
------------------



Faceted maps, described in Section [9\.2\.7](/adv-map#faceted-maps), can show how spatial distributions of variables change (e.g., over time), but the approach has disadvantages.
Facets become tiny when there are many of them.
Furthermore, the fact that each facet is physically separated on the screen or page means that subtle differences between facets can be hard to detect.


Animated maps solve these issues.
Although they depend on digital publication, this is becoming less of an issue as more and more content moves online.
Animated maps can still enhance paper reports: you can always link readers to a webpage containing an animated (or interactive) version of a printed map to help make it come alive.
There are several ways to generate animations in R, including with animation packages such as **gganimate**, which builds on **ggplot2** (see Section [9\.6](/adv-map#other-mapping-packages)).
This section focuses on creating animated maps with **tmap** because its syntax will be familiar from previous sections and the flexibility of the approach.


Figure [9\.15](/adv-map#fig:urban-animated) is a simple example of an animated map.
Unlike the faceted plot, it does not squeeze multiple maps into a single screen and allows the reader to see how the spatial distribution of the world’s most populous agglomerations evolve over time (see the book’s website for the animated version).





FIGURE 9\.15: Animated map showing the top 30 largest urban agglomerations from 1950 to 2030 based on population projects by the United Nations. Animated version available online at: r.geocompx.org.




The animated map illustrated in Figure [9\.15](/adv-map#fig:urban-animated) can be created using the same **tmap** techniques that generate faceted maps, demonstrated in Section [9\.2\.7](/adv-map#faceted-maps).
There are two differences, however, related to arguments in `[tm_facets_wrap()](https://r-tmap.github.io/tmap/reference/tm_facets.html)`:


* `nrow = 1, ncol = 1` are added to keep one moment in time as one layer
* `free.coords = FALSE`, which maintains the map extent for each map iteration


These additional arguments are demonstrated in the subsequent code chunk53:



```

urb_anim = [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(world) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)() + 
  [tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(urban_agglomerations) + [tm_symbols](https://r-tmap.github.io/tmap/reference/tm_symbols.html)(size = "population_millions") +
  [tm_facets_wrap](https://r-tmap.github.io/tmap/reference/tm_facets.html)(by = "year", nrow = 1, ncol = 1, free.coords = FALSE)
```

The resulting `urb_anim` represents a set of separate maps for each year.
The final stage is to combine them and save the result as a `.gif` file with `[tmap_animation()](https://r-tmap.github.io/tmap/reference/tmap_animation.html)`.
The following command creates the animation illustrated in Figure [9\.15](/adv-map#fig:urban-animated), with a few elements missing, that we will add during the exercises:



```

[tmap_animation](https://r-tmap.github.io/tmap/reference/tmap_animation.html)(urb_anim, filename = "urb_anim.gif", delay = 25)
```

Another illustration of the power of animated maps is provided in Figure [9\.16](/adv-map#fig:animus).
This shows the development of states in the United States, which first formed in the east and then incrementally to the west and finally into the interior.
Code to reproduce this map can be found in the script `code/09-usboundaries.R` in the book GitHub repository.




![Animated map showing population growth, state formation and boundary changes in the United States, 1790-2010. Animated version available online at r.geocompx.org.](opensource/tidytuesday/2021-11-02/images/0.png)
FIGURE 9\.16: Animated map showing population growth, state formation and boundary changes in the United States, 1790\-2010\. Animated version available online at r.geocompx.org.






9\.4 Interactive maps
---------------------



While static and animated maps can enliven geographic datasets, interactive maps can take them to a new level.
Interactivity can take many forms, the most common and useful of which is the ability to pan around and zoom into any part of a geographic dataset overlaid on a ‘web map’ to show context.
Less advanced interactivity levels include pop\-ups which appear when you click on different features, a kind of interactive label.
More advanced levels of interactivity include the ability to tilt and rotate maps, as demonstrated in the **mapdeck** example below, and the provision of “dynamically linked” sub\-plots which automatically update when the user pans and zooms ([Pezanowski et al. 2018](/references#ref-pezanowski_senseplace3_2018)).


The most important type of interactivity, however, is the display of geographic data on interactive or ‘slippy’ web maps.
The release of the **leaflet** package in 2015 (that uses the leaflet JavaScript library) revolutionized interactive web map creation from within R, and a number of packages have built on these foundations adding new features (e.g., **leaflet.extras2**) and making the creation of web maps as simple as creating static maps (e.g., **mapview** and **tmap**).
This section illustrates each approach in the opposite order.
We will explore how to make slippy maps with **tmap** (the syntax of which we have already learned), **mapview**, **mapdeck** and finally **leaflet** (which provides low\-level control over interactive maps).


A unique feature of **tmap** mentioned in Section [9\.2](/adv-map#static-maps) is its ability to create static and interactive maps using the same code.
Maps can be viewed interactively at any point by switching to view mode, using the command `tmap_mode("view")`.
This is demonstrated in the code below, which creates an interactive map of New Zealand based on the `tmap` object `map_nz`, created in Section [9\.2\.2](/adv-map#map-obj), and illustrated in Figure [9\.17](/adv-map#fig:tmview):



```

[tmap_mode](https://r-tmap.github.io/tmap/reference/tmap_mode.html)("view")
map_nz
```






FIGURE 9\.17: Interactive map of New Zealand created with tmap in view mode. Interactive version available online at: r.geocompx.org.




Now that the interactive mode has been ‘turned on’, all maps produced with **tmap** will launch (another way to create interactive maps is with the `[tmap_leaflet()](https://r-tmap.github.io/tmap/reference/tmap_leaflet.html)` function).
Notable features of this interactive mode include the ability to specify the basemap with `[tm_basemap()](https://r-tmap.github.io/tmap/reference/tm_basemap.html)` (or `[tmap_options()](https://r-tmap.github.io/tmap/reference/tmap_options.html)`) as demonstrated below (result not shown):



```

map_nz + [tm_basemap](https://r-tmap.github.io/tmap/reference/tm_basemap.html)(server = "OpenTopoMap")
```

An impressive and little\-known feature of **tmap**’s view mode is that it also works with faceted plots.
The argument `sync` in `[tm_facets_wrap()](https://r-tmap.github.io/tmap/reference/tm_facets.html)` can be used in this case to produce multiple maps with synchronized zoom and pan settings, as illustrated in Figure [9\.18](/adv-map#fig:sync), which was produced by the following code:



```

world_coffee = [left_join](https://dplyr.tidyverse.org/reference/mutate-joins.html)(world, coffee_data, by = "name_long")
facets = [c](https://rdrr.io/r/base/c.html)("coffee_production_2016", "coffee_production_2017")
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(world_coffee) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)(facets) + 
  [tm_facets_wrap](https://r-tmap.github.io/tmap/reference/tm_facets.html)(nrow = 1, sync = TRUE)
```




FIGURE 9\.18: Faceted interactive maps of global coffee production in 2016 and 2017 in sync, demonstrating tmap’s view mode in action.




Switch **tmap** back to plotting mode with the same function:



```

[tmap_mode](https://r-tmap.github.io/tmap/reference/tmap_mode.html)("plot")
#> ℹ tmap mode set to "plot".
```

If you are not proficient with **tmap**, the quickest way to create interactive maps in R may be with **mapview**.
The following ‘one liner’ is a reliable way to interactively explore a wide range of geographic data formats:



```

mapview::[mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(nz)
```




FIGURE 9\.19: Illustration of mapview in action.




**mapview** has a concise syntax, yet, it is powerful.
By default, it has some standard GIS functionality such as mouse position information, attribute queries (via pop\-ups), scale bar, and zoom\-to\-layer buttons.
It also offers advanced controls including the ability to ‘burst’ datasets into multiple layers and the addition of multiple layers with `+` followed by the name of a geographic object.
Additionally, it provides automatic coloring of attributes via the `zcol` argument.
In essence, it can be considered a data\-driven **leaflet** API (see below for more information about **leaflet**).
Given that **mapview** always expects a spatial object (including `sf` and `SpatRaster`) as its first argument, it works well at the end of piped expressions.
Consider the following example where **sf** is used to intersect lines and polygons and then is visualized with **mapview** (Figure [9\.20](/adv-map#fig:mapview2)).



```

[library](https://rdrr.io/r/base/library.html)([mapview](https://github.com/r-spatial/mapview))
oberfranken = [subset](https://rspatial.github.io/terra/reference/subset.html)(franconia, district == "Oberfranken")
trails |>
  [st_transform](https://r-spatial.github.io/sf/reference/st_transform.html)([st_crs](https://r-spatial.github.io/sf/reference/st_crs.html)(oberfranken)) |>
  [st_intersection](https://r-spatial.github.io/sf/reference/geos_binary_ops.html)(oberfranken) |>
  [st_collection_extract](https://r-spatial.github.io/sf/reference/st_collection_extract.html)("LINESTRING") |>
  [mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(color = "red", lwd = 3, layer.name = "trails") +
  [mapview](https://rdrr.io/pkg/mapview/man/mapView.html)(franconia, zcol = "district") +
  breweries
```




FIGURE 9\.20: Using mapview at the end of an sf\-based pipe expression.




One important thing to keep in mind is that **mapview** layers are added via the `+` operator (similar to **ggplot2** or **tmap**).
By default, **mapview** uses the leaflet JavaScript library to render the output maps, which is user\-friendly and has a lot of features.
However, some alternative rendering libraries could be more performant (work more smoothly on larger datasets).
**mapview** allows to set alternative rendering libraries (`"leafgl"` and `"mapdeck"`) in the `[mapviewOptions()](https://rdrr.io/pkg/mapview/man/mapviewOptions.html)`.54
For further information on **mapview**, see the package’s website at: [r\-spatial.github.io/mapview/](https://r-spatial.github.io/mapview/articles/).


There are other ways to create interactive maps with R.
The **googleway** package, for example, provides an interactive mapping interface that is flexible and extensible
(see the [`googleway-vignette`](https://cran.r-project.org/package=googleway/vignettes/googleway-vignette.html) for details).
Another approach by the same author is **[mapdeck](https://github.com/SymbolixAU/mapdeck)**, which provides access to Uber’s `Deck.gl` framework.
Its use of WebGL enables it to interactively visualize large datasets up to millions of points.
The package uses Mapbox [access tokens](https://docs.mapbox.com/help/getting-started/access-tokens/), which you must register for before using the package.



Note that the following block assumes the access token is stored in your R environment as `MAPBOX=your_unique_key`.
This can be added with `[usethis::edit_r_environ()](https://usethis.r-lib.org/reference/edit.html)`.

A unique feature of **mapdeck** is its provision of interactive 2\.5D perspectives, illustrated in Figure [9\.21](/adv-map#fig:mapdeck).
This means you can can pan, zoom and rotate around the maps, and view the data ‘extruded’ from the map.
Figure [9\.21](/adv-map#fig:mapdeck), generated by the following code chunk, visualizes road traffic crashes in the UK, with bar height representing casualties per area.



```

[library](https://rdrr.io/r/base/library.html)([mapdeck](https://symbolixau.github.io/mapdeck/articles/mapdeck.html))
[set_token](https://rdrr.io/pkg/mapdeck/man/set_token.html)([Sys.getenv](https://rdrr.io/r/base/Sys.getenv.html)("MAPBOX"))
crash_data = [read.csv](https://rdrr.io/r/utils/read.table.html)("https://git.io/geocompr-mapdeck")
crash_data = [na.omit](https://rspatial.github.io/terra/reference/na.omit.html)(crash_data)
ms = [mapdeck_style](https://rdrr.io/pkg/mapdeck/man/mapdeck_style.html)("dark")
[mapdeck](https://rdrr.io/pkg/mapdeck/man/mapdeck.html)(style = ms, pitch = 45, location = [c](https://rdrr.io/r/base/c.html)(0, 52), zoom = 4) |>
  [add_grid](https://rdrr.io/pkg/mapdeck/man/add_grid.html)(data = crash_data, lat = "lat", lon = "lng", cell_size = 1000,
           elevation_scale = 50, colour_range = [hcl.colors](https://rdrr.io/r/grDevices/palettes.html)(6, "plasma"))
```




FIGURE 9\.21: Map generated by mapdeck, representing road traffic casualties across the UK. Height of 1\-km cells represents number of crashes.




You can zoom and drag the map in the browser, in addition to rotating and tilting it when pressing `Cmd`/`Ctrl`.
Multiple layers can be added with the pipe operator, as demonstrated in the [`mapdeck` vignettes](https://cran.r-project.org/package=mapdeck/vignettes/mapdeck.html).
**mapdeck** also supports `sf` objects, as can be seen by replacing the `[add_grid()](https://rdrr.io/pkg/mapdeck/man/add_grid.html)` function call in the preceding code chunk with `add_polygon(data = lnd, layer_id = "polygon_layer")`, to add polygons representing London to an interactive tilted map.


Last is **leaflet** which is the most mature and widely used interactive mapping package in R.
**leaflet** provides a relatively low\-level interface to the Leaflet JavaScript library and many of its arguments can be understood by reading the documentation of the original JavaScript library (see [leafletjs.com](https://leafletjs.com/)).


Leaflet maps are created with `[leaflet()](https://rstudio.github.io/leaflet/reference/leaflet.html)`, the result of which is a `leaflet` map object which can be piped to other **leaflet** functions.
This allows multiple map layers and control settings to be added interactively, as demonstrated in the code below which generates Figure [9\.22](/adv-map#fig:leaflet) (see [rstudio.github.io/leaflet/](https://rstudio.github.io/leaflet/) for details).



```

pal = [colorNumeric](https://rstudio.github.io/leaflet/reference/colorNumeric.html)("RdYlBu", domain = cycle_hire$nbikes)
[leaflet](https://rstudio.github.io/leaflet/reference/leaflet.html)(data = cycle_hire) |> 
  [addProviderTiles](https://rstudio.github.io/leaflet/reference/addProviderTiles.html)(providers$CartoDB.Positron) |>
  [addCircles](https://rstudio.github.io/leaflet/reference/map-layers.html)(col = ~pal(nbikes), opacity = 0.9) |> 
  [addPolygons](https://rstudio.github.io/leaflet/reference/map-layers.html)(data = lnd, fill = FALSE) |> 
  [addLegend](https://rstudio.github.io/leaflet/reference/addLegend.html)(pal = pal, values = ~nbikes) |> 
  [setView](https://rstudio.github.io/leaflet/reference/map-methods.html)(lng = -0.1, 51.5, zoom = 12) |> 
  [addMiniMap](https://rstudio.github.io/leaflet/reference/addMiniMap.html)()
```




FIGURE 9\.22: The leaflet package in action, showing cycle hire points in London. See interactive version [online](https://geocompr.github.io/img/leaflet.html).






9\.5 Mapping applications
-------------------------



The interactive web maps demonstrated in Section [9\.4](/adv-map#interactive-maps) can go far.
Careful selection of layers to display, basemaps and pop\-ups can be used to communicate the main results of many projects involving geocomputation.
But the web mapping approach to interactivity has limitations:


* Although the map is interactive in terms of panning, zooming and clicking, the code is static, meaning the user interface is fixed
* All map content is generally static in a web map, meaning that web maps cannot scale to handle large datasets easily
* Additional layers of interactivity, such a graphs showing relationships between variables and ‘dashboards’, are difficult to create using the web mapping\-approach


Overcoming these limitations involves going beyond static web mapping and toward geospatial frameworks and map servers.
Products in this field include [GeoDjango](https://docs.djangoproject.com/en/4.0/ref/contrib/gis/) (which extends the Django web framework and is written in [Python](https://github.com/django/django)), [MapServer](https://github.com/mapserver/mapserver) (a framework for developing web applications, largely written in C and C\+\+) and [GeoServer](https://github.com/geoserver/geoserver) (a mature and powerful map server written in Java).
Each of these is scalable, enabling maps to be served to thousands of people daily, assuming there is sufficient public interest in your maps!
The bad news is that such server\-side solutions require much skilled developer time to set up and maintain, often involving teams of people with roles such as a dedicated geospatial database administrator ([DBA](https://wiki.gis.com/wiki/index.php/Database_administrator)).


Fortunately for R programmers, web mapping applications can now be rapidly created with **shiny**.
As described in the open source book [Mastering Shiny](https://mastering-shiny.org/), **shiny** is an R package and framework for converting R code into interactive web applications ([Wickham 2021](/references#ref-wickham_mastering_2021)).
You can embed interactive maps in shiny apps thanks to functions such as [`leaflet::renderLeaflet()`](https://rstudio.github.io/leaflet/shiny.html).
This section gives some context, teaches the basics of **shiny** from a web mapping perspective, and culminates in a full\-screen mapping application in less than 100 lines of code.


**shiny** is well documented at [shiny.posit.co](https://shiny.posit.co/), which highlights the two components of every **shiny** app: ‘front end’ (the bit the user sees) and ‘back end’ code.
In **shiny** apps, these elements are typically created in objects named `ui` and `server` within an R script named `app.R`, which lives in an ‘app folder’.
This allows web mapping applications to be represented in a single file, such as the [`CycleHireApp/app.R`](https://github.com/geocompx/geocompr/blob/main/apps/CycleHireApp/app.R) file in the book’s GitHub repo.



In **shiny** apps these are often split into `ui.R` (short for user interface) and `server.R` files, naming conventions used by `shiny-server`, a server\-side Linux application for serving shiny apps on public\-facing websites.
`shiny-server` also serves apps defined by a single `app.R` file in an ‘app folder’.
Learn more at: [https://github.com/rstudio/shiny\-server](https://github.com/rstudio/shiny-server).

Before considering large apps, it is worth seeing a minimal example, named ‘lifeApp’, in action.55
The code below defines and launches — with the command `[shinyApp()](https://rdrr.io/pkg/shiny/man/shinyApp.html)` — a lifeApp, which provides an interactive slider allowing users to make countries appear with progressively lower levels of life expectancy (see Figure [9\.23](/adv-map#fig:lifeApp)):



```

[library](https://rdrr.io/r/base/library.html)([shiny](https://shiny.posit.co/))    # for shiny apps
[library](https://rdrr.io/r/base/library.html)([leaflet](https://rstudio.github.io/leaflet/))  # renderLeaflet function
[library](https://rdrr.io/r/base/library.html)([spData](https://jakubnowosad.com/spData/))   # loads the world dataset 
ui = [fluidPage](https://rdrr.io/pkg/shiny/man/fluidPage.html)(
  [sliderInput](https://rdrr.io/pkg/shiny/man/sliderInput.html)(inputId = "life", "Life expectancy", 49, 84, value = 80),
      [leafletOutput](https://rstudio.github.io/leaflet/reference/map-shiny.html)(outputId = "map")
  )
server = function(input, output) {
  output$map = [renderLeaflet](https://rstudio.github.io/leaflet/reference/map-shiny.html)({
    [leaflet](https://rstudio.github.io/leaflet/reference/leaflet.html)() |> 
      # addProviderTiles("OpenStreetMap.BlackAndWhite") |>
      [addPolygons](https://rstudio.github.io/leaflet/reference/map-layers.html)(data = world[world$lifeExp < input$life, ])})
}
[shinyApp](https://rdrr.io/pkg/shiny/man/shinyApp.html)(ui, server)
```




FIGURE 9\.23: Screenshot showing minimal example of a web mapping application created with shiny.




The **user interface** (`ui`) of lifeApp is created by `[fluidPage()](https://rdrr.io/pkg/shiny/man/fluidPage.html)`.
This contains input and output ‘widgets’ — in this case, a `[sliderInput()](https://rdrr.io/pkg/shiny/man/sliderInput.html)` (many other `*Input()` functions are available) and a `[leafletOutput()](https://rstudio.github.io/leaflet/reference/map-shiny.html)`.
These are arranged row\-wise by default, explaining why the slider interface is placed directly above the map in Figure [9\.23](/adv-map#fig:lifeApp) (see `[?column](https://rdrr.io/pkg/shiny/man/column.html)` for adding content column\-wise).


The **server side** (`server`) is a function with `input` and `output` arguments.
`output` is a list of objects containing elements generated by `render*()` function — `[renderLeaflet()](https://rstudio.github.io/leaflet/reference/map-shiny.html)` which in this example generates `output$map`.
Input elements such as `input$life` referred to in the server must relate to elements that exist in the `ui` — defined by `inputId = "life"` in the code above.
The function `[shinyApp()](https://rdrr.io/pkg/shiny/man/shinyApp.html)` combines both the `ui` and `server` elements and serves the results interactively via a new R process.
When you move the slider in the map shown in Figure [9\.23](/adv-map#fig:lifeApp), you are actually causing R code to re\-run, although this is hidden from view in the user interface.


Building on this basic example and knowing where to find help (see `[?shiny](https://rdrr.io/pkg/shiny/man/shiny-package.html)`), the best way forward now may be to stop reading and start programming!
The recommended next step is to open the previously mentioned [`CycleHireApp/app.R`](https://github.com/geocompx/geocompr/blob/main/apps/CycleHireApp/app.R) script in an integrated development environment (IDE) of choice, modify it and re\-run it repeatedly.
The example contains some of the components of a web mapping application implemented in **shiny** and should ‘shine’ a light on how they behave.


The `CycleHireApp/app.R` script contains **shiny** functions that go beyond those demonstrated in the simple ‘lifeApp’ example, deployed at [shiny.robinlovelace.net/CycleHireApp](https://shiny.robinlovelace.net/CycleHireApp).
These include `[reactive()](https://rdrr.io/pkg/shiny/man/reactive.html)` and `[observe()](https://rdrr.io/pkg/shiny/man/observe.html)`, (for creating outputs that respond to the user interface, see `[?reactive](https://rdrr.io/pkg/shiny/man/reactive.html)`) and `[leafletProxy()](https://rstudio.github.io/leaflet/reference/leafletProxy.html)` (for modifying a `leaflet` object that has already been created).
Such elements enable web mapping applications implemented in **shiny** ([Lovelace et al. 2017](/references#ref-lovelace_propensity_2017)).
A range of ‘events’ can be programmed including advanced functionality such as drawing new layers or subsetting data, as described in the shiny section of RStudio’s **leaflet** [website](https://rstudio.github.io/leaflet/shiny.html).



There are a number of ways to run a **shiny** app.
For RStudio users, the simplest way is probably to click on the ‘Run App’ button located in the top right of the source pane when an `app.R`, `ui.R` or `server.R` script is open.
**shiny** apps can also be initiated by using `[runApp()](https://rdrr.io/pkg/shiny/man/runApp.html)` with the first argument being the folder containing the app code and data: `runApp("CycleHireApp")` in this case (which assumes a folder named `CycleHireApp` containing the `app.R` script is in your working directory).
You can also launch apps from a Unix command line with the command `Rscript -e 'shiny::runApp("CycleHireApp")'`.

Experimenting with apps such as `CycleHireApp` will build not only your knowledge of web mapping applications in R, but also your practical skills.
Changing the contents of `[setView()](https://rstudio.github.io/leaflet/reference/map-methods.html)`, for example, will change the starting bounding box that the user sees when the app is initiated.
Such experimentation should not be done at random, but with reference to relevant documentation, starting with `[?shiny](https://rdrr.io/pkg/shiny/man/shiny-package.html)`, and motivated by a desire to solve problems such as those posed in the exercises.


**shiny** used in this way can make prototyping mapping applications faster and more accessible than ever before (deploying **shiny** apps, <https://shiny.posit.co/deploy/>, is a separate topic beyond the scope of this chapter).
Even if your applications are eventually deployed using different technologies, **shiny** undoubtedly allows web mapping applications to be developed in relatively few lines of code (86 in the case of CycleHireApp).
That does not stop shiny apps getting rather large.
The Propensity to Cycle Tool (PCT) hosted at [pct.bike](https://www.pct.bike/), for example, is a national mapping tool funded by the UK’s Department for Transport.
The PCT is used by dozens of people each day and has multiple interactive elements based on more than 1000 lines of [code](https://github.com/npct/pct-shiny/blob/master/regions_www/m/server.R) ([Lovelace et al. 2017](/references#ref-lovelace_propensity_2017)).


While such apps undoubtedly take time and effort to develop, **shiny** provides a framework for reproducible prototyping that should aid the development process.
One potential problem with the ease of developing prototypes with **shiny** is the temptation to start programming too early, before the purpose of the mapping application has been envisioned in detail.
For that reason, despite advocating **shiny**, we recommend starting with the longer established technology of a pen and paper as the first stage for interactive mapping projects.
This way your prototype web applications should be limited not by technical considerations, but by your motivations and imagination.







FIGURE 9\.24: CycleHireApp, a simple web mapping application for finding the closest cycle hiring station based on your location and requirement of cycles. Interactive version available online at: r.geocompx.org.






9\.6 Other mapping packages
---------------------------


**tmap** provides a powerful interface for creating a wide range of static maps (Section [9\.2](/adv-map#static-maps)) and also supports interactive maps (Section [9\.4](/adv-map#interactive-maps)).
But there are many other options for creating maps in R.
The aim of this section is to provide a taste of some of these and pointers for additional resources: map\-making is a surprisingly active area of R package development, so there is more to learn than can be covered here.


The most mature option is to use `[plot()](https://rspatial.github.io/terra/reference/plot.html)` methods provided by core spatial packages **sf** and **terra**, covered in Sections [2\.2\.3](/spatial-class#basic-map) and [2\.3\.3](/spatial-class#basic-map-raster), respectively.
What we have not mentioned in those sections was that plot methods for vector and raster objects can be combined when the results draw onto the same plot area (elements such as keys in **sf** plots and multi\-band rasters will interfere with this).
This behavior is illustrated in the subsequent code chunk which generates Figure [9\.25](/adv-map#fig:nz-plot).
`[plot()](https://rspatial.github.io/terra/reference/plot.html)` has many other options which can be explored by following links in the `[?plot](https://r-spatial.github.io/sf/reference/plot.html)` help page and the fifth **sf** vignette [`sf5`](https://cran.r-project.org/package=sf/vignettes/sf5.html).



```

g = [st_graticule](https://r-spatial.github.io/sf/reference/st_graticule.html)(nz, lon = [c](https://rdrr.io/r/base/c.html)(170, 175), lat = [c](https://rdrr.io/r/base/c.html)(-45, -40, -35))
[plot](https://rspatial.github.io/terra/reference/plot.html)(nz_water, graticule = g, axes = TRUE, col = "blue")
terra::[plot](https://rspatial.github.io/terra/reference/plot.html)(nz_elev / 1000, add = TRUE, axes = FALSE)
[plot](https://rspatial.github.io/terra/reference/plot.html)([st_geometry](https://r-spatial.github.io/sf/reference/st_geometry.html)(nz), add = TRUE)
```




FIGURE 9\.25: Map of New Zealand created with plot(). The legend to the right refers to elevation (1000 m above sea level).




The **tidyverse** plotting package **ggplot2** also supports `sf` objects with `[geom_sf()](https://ggplot2.tidyverse.org/reference/ggsf.html)`.
The syntax is similar to that used by **tmap**:
an initial `[ggplot()](https://ggplot2.tidyverse.org/reference/ggplot.html)` call is followed by one or more layers, that are added with `+ geom_*()`, where `*` represents a layer type such as `[geom_sf()](https://ggplot2.tidyverse.org/reference/ggsf.html)` (for `sf` objects) or `geom_points()` (for points).


**ggplot2** plots graticules by default.
The default settings for the graticules can be overridden using `[scale_x_continuous()](https://ggplot2.tidyverse.org/reference/scale_continuous.html)`, `[scale_y_continuous()](https://ggplot2.tidyverse.org/reference/scale_continuous.html)` or [`coord_sf(datum = NA)`](https://github.com/tidyverse/ggplot2/issues/2071).
Other notable features include the use of unquoted variable names encapsulated in `[aes()](https://ggplot2.tidyverse.org/reference/aes.html)` to indicate which aesthetics vary and switching data sources using the `data` argument, as demonstrated in the code chunk below which creates Figure [9\.26](/adv-map#fig:nz-gg2):



```

[library](https://rdrr.io/r/base/library.html)([ggplot2](https://ggplot2.tidyverse.org))
g1 = [ggplot](https://ggplot2.tidyverse.org/reference/ggplot.html)() + [geom_sf](https://ggplot2.tidyverse.org/reference/ggsf.html)(data = nz, [aes](https://ggplot2.tidyverse.org/reference/aes.html)(fill = Median_income)) +
  [geom_sf](https://ggplot2.tidyverse.org/reference/ggsf.html)(data = nz_height) +
  [scale_x_continuous](https://ggplot2.tidyverse.org/reference/scale_continuous.html)(breaks = [c](https://rdrr.io/r/base/c.html)(170, 175))
g1
```

Another benefit of maps based on **ggplot2** is that they can easily be given a level of interactivity when printed using the function `ggplotly()` from the **plotly** package.
Try `plotly::ggplotly(g1)`, for example, and compare the result with other **plotly** mapping functions described at: [blog.cpsievert.me](https://blog.cpsievert.me/2018/03/30/visualizing-geo-spatial-data-with-sf-and-plotly/).


An advantage of **ggplot2** is that it has a strong user community and many add\-on packages.
It includes **ggspatial**, which enhances **ggplot2**’s mapping capabilities by providing options to add a north arrow (`[annotation_north_arrow()](https://paleolimbot.github.io/ggspatial/reference/annotation_north_arrow.html)`) and a scale bar (`[annotation_scale()](https://paleolimbot.github.io/ggspatial/reference/annotation_scale.html)`), or to add background tiles (`[annotation_map_tile()](https://paleolimbot.github.io/ggspatial/reference/annotation_map_tile.html)`).
It also accepts various spatial data classes with `[layer_spatial()](https://paleolimbot.github.io/ggspatial/reference/layer_spatial.html)`.
Thus, we are able to plot `SpatRaster` objects from **terra** using this function as seen in Figure [9\.26](/adv-map#fig:nz-gg2).



```

[library](https://rdrr.io/r/base/library.html)([ggspatial](https://paleolimbot.github.io/ggspatial/))
[ggplot](https://ggplot2.tidyverse.org/reference/ggplot.html)() + 
  [layer_spatial](https://paleolimbot.github.io/ggspatial/reference/layer_spatial.html)(nz_elev) +
  [geom_sf](https://ggplot2.tidyverse.org/reference/ggsf.html)(data = nz, fill = NA) +
  [annotation_scale](https://paleolimbot.github.io/ggspatial/reference/annotation_scale.html)() +
  [scale_x_continuous](https://ggplot2.tidyverse.org/reference/scale_continuous.html)(breaks = [c](https://rdrr.io/r/base/c.html)(170, 175)) +
  [scale_fill_continuous](https://ggplot2.tidyverse.org/reference/scale_colour_continuous.html)(na.value = NA)
```




FIGURE 9\.26: Comparison of map of New Zealand created with ggplot2 alone (left) and ggplot2 and ggspatial (right).




At the same time, **ggplot2** has a few drawbacks, for example the `[geom_sf()](https://ggplot2.tidyverse.org/reference/ggsf.html)` function is not always able to create a desired legend to use from the spatial [data](https://github.com/tidyverse/ggplot2/issues/2037).
Good additional **ggplot2** resources can be found in the open source [ggplot2 book](https://ggplot2-book.org/) ([Wickham 2016](/references#ref-wickham_ggplot2_2016)) and in the descriptions of the multitude of ‘**gg**packages’ such as **ggrepel** and **tidygraph**.


We have covered mapping with **sf**, **terra** and **ggplot2** first because these packages are highly flexible, allowing for the creation of a wide range of static maps.
Before we cover mapping packages for plotting a specific type of map (in the next paragraph), it is worth considering alternatives to the packages already covered for general\-purpose mapping (Table [9\.1](/adv-map#tab:map-gpkg)).





TABLE 9\.1: TABLE 9\.2: Selected general\-purpose mapping packages.

| Package | Title |
| --- | --- |
| ggplot2 | Create Elegant Data Visualisations Using the Grammar of Graphics |
| googleway | Accesses Google Maps APIs to Retrieve Data and Plot Maps |
| ggspatial | Spatial Data Framework for ggplot2 |
| leaflet | Create Interactive Web Maps with Leaflet |
| mapview | Interactive Viewing of Spatial Data in R |
| plotly | Create Interactive Web Graphics via ‘plotly.js’ |
| rasterVis | Visualization Methods for Raster Data |
| tmap | Thematic Maps |


Table [9\.1](/adv-map#tab:map-gpkg) shows a range of mapping packages that are available, and there are many others not listed in this table.
Of note is **mapsf**, which can generate a range of geographic visualizations including choropleth, ‘proportional symbol’ and ‘flow’ maps.
These are documented in the [`mapsf`](https://cran.r-project.org/package=mapsf/vignettes/mapsf.html) vignette.


Several packages focus on specific map types, as illustrated in Table [9\.3](/adv-map#tab:map-spkg).
Such packages create cartograms that distort geographical space, create line maps, transform polygons into regular or hexagonal grids, visualize complex data on grids representing geographic topologies, and create 3D visualizations.





TABLE 9\.3: Selected specific\-purpose mapping packages, with associated metrics.
| Package | Title |
| --- | --- |
| cartogram | Create Cartograms with R |
| geogrid | Turn Geospatial Polygons into Regular or Hexagonal Grids |
| geofacet | ‘ggplot2’ Faceting Utilities for Geographical Data |
| linemap | Line Maps |
| tanaka | Design Shaded Contour Lines (or Tanaka) Maps |
| rayshader | Create Maps and Visualize Data in 2D and 3D |


All of the aforementioned packages, however, have different approaches for data preparation and map creation.
In the next paragraph, we focus solely on the **cartogram** package ([Jeworutzki 2023](/references#ref-R-cartogram)).
Therefore, we suggest to read the [geogrid](https://github.com/jbaileyh/geogrid), [geofacet](https://github.com/hafen/geofacet), [linemap](https://github.com/riatelab/linemap), [tanaka](https://github.com/riatelab/tanaka), and [rayshader](https://github.com/tylermorganwall/rayshader) documentations to learn more about them.


A cartogram is a map in which the geometry is proportionately distorted to represent a mapping variable.
Creation of this type of map is possible in R with **cartogram**, which allows for creating contiguous and non\-contiguous area cartograms.
It is not a mapping package per se, but it allows for construction of distorted spatial objects that could be plotted using any generic mapping package.


The `[cartogram_cont()](https://rdrr.io/pkg/cartogram/man/cartogram_cont.html)` function creates contiguous area cartograms.
It accepts an `sf` object and name of the variable (column) as inputs.
Additionally, it is possible to modify the `intermax` argument – maximum number of iterations for the cartogram transformation.
For example, we could represent median income in New Zeleand’s regions as a contiguous cartogram (Figure [9\.27](/adv-map#fig:cartomap1), right panel) as follows:



```

[library](https://rdrr.io/r/base/library.html)([cartogram](https://github.com/sjewo/cartogram))
nz_carto = [cartogram_cont](https://rdrr.io/pkg/cartogram/man/cartogram_cont.html)(nz, "Median_income", itermax = 5)
[tm_shape](https://r-tmap.github.io/tmap/reference/tm_shape.html)(nz_carto) + [tm_polygons](https://r-tmap.github.io/tmap/reference/tm_polygons.html)("Median_income")
```




FIGURE 9\.27: Comparison of standard map (left) and contiguous area cartogram (right).




**cartogram** also offers creation of non\-contiguous area cartograms using `[cartogram_ncont()](https://rdrr.io/pkg/cartogram/man/cartogram_ncont.html)` and Dorling cartograms using `[cartogram_dorling()](https://rdrr.io/pkg/cartogram/man/cartogram_dorling.html)`.
Non\-contiguous area cartograms are created by scaling down each region based on the provided weighting variable.
Dorling cartograms consist of circles with their area proportional to the weighting variable.
The code chunk below demonstrates creation of non\-contiguous area and Dorling cartograms of US states’ population (Figure [9\.28](/adv-map#fig:cartomap2)):



```

us_states9311 = [st_transform](https://r-spatial.github.io/sf/reference/st_transform.html)(us_states, "EPSG:9311")
us_states9311_ncont = [cartogram_ncont](https://rdrr.io/pkg/cartogram/man/cartogram_ncont.html)(us_states9311, "total_pop_15")
us_states9311_dorling = [cartogram_dorling](https://rdrr.io/pkg/cartogram/man/cartogram_dorling.html)(us_states9311, "total_pop_15")
```




FIGURE 9\.28: Comparison of non\-contiguous area cartogram (left) and Dorling cartogram (right).






9\.7 Exercises
--------------


These exercises rely on a new object, `africa`.
Create it using the `world` and `worldbank_df` datasets from the **spData** package as follows:



```

[library](https://rdrr.io/r/base/library.html)([spData](https://jakubnowosad.com/spData/))
africa = world |> 
  [filter](https://dplyr.tidyverse.org/reference/filter.html)(continent == "Africa", ![is.na](https://rdrr.io/r/base/NA.html)(iso_a2)) |> 
  [left_join](https://dplyr.tidyverse.org/reference/mutate-joins.html)(worldbank_df, by = "iso_a2") |> 
  [select](https://dplyr.tidyverse.org/reference/select.html)(name, subregion, gdpPercap, HDI, pop_growth) |> 
  [st_transform](https://r-spatial.github.io/sf/reference/st_transform.html)("ESRI:102022") |> 
  [st_make_valid](https://r-spatial.github.io/sf/reference/valid.html)() |> 
  [st_collection_extract](https://r-spatial.github.io/sf/reference/st_collection_extract.html)("POLYGON")
```

We will also use `zion` and `nlcd` datasets from **spDataLarge**:



```

zion = [read_sf](https://r-spatial.github.io/sf/reference/st_read.html)(([system.file](https://rdrr.io/r/base/system.file.html)("vector/zion.gpkg", package = "spDataLarge")))
nlcd = [rast](https://rspatial.github.io/terra/reference/rast.html)([system.file](https://rdrr.io/r/base/system.file.html)("raster/nlcd.tif", package = "spDataLarge"))
```

E1\. Create a map showing the geographic distribution of the Human Development Index (`HDI`) across Africa with base **graphics** (hint: use `[plot()](https://rspatial.github.io/terra/reference/plot.html)`) and **tmap** packages (hint: use `tm_shape(africa) + ...`).


* Name two advantages of each based on the experience.
* Name three other mapping packages and an advantage of each.
* Bonus: create three more maps of Africa using these three other packages.


E2\. Extend the **tmap** created for the previous exercise so the legend has three bins: “High” (`HDI` above 0\.7\), “Medium” (`HDI` between 0\.55 and 0\.7\) and “Low” (`HDI` below 0\.55\).
Bonus: improve the map aesthetics, for example by changing the legend title, class labels and color palette.


E3\. Represent `africa`’s subregions on the map.
Change the default color palette and legend title.
Next, combine this map and the map created in the previous exercise into a single plot.


E4\. Create a land cover map of Zion National Park.


* Change the default colors to match your perception of the land cover categories
* Add a scale bar and north arrow and change the position of both to improve the map’s aesthetic appeal
* Bonus: Add an inset map of Zion National Park’s location in the context of the state of Utah. (Hint: an object representing Utah can be subset from the `us_states` dataset.)


E5\. Create facet maps of countries in Eastern Africa:


* With one facet showing HDI and the other representing population growth (hint: using variables `HDI` and `pop_growth`, respectively)
* With a ‘small multiple’ per country


E6\. Building on the previous facet map examples, create animated maps of East Africa:


* Showing each country in order
* Showing each country in order with a legend showing the HDI


E7\. Create an interactive map of HDI in Africa:


* With **tmap**
* With **mapview**
* With **leaflet**
* Bonus: For each approach, add a legend (if not automatically provided) and a scale bar


E8\. Sketch on paper ideas for a web mapping application that could be used to make transport or land\-use policies more evidence\-based:


* In the city you live, for a couple of users per day
* In the country you live, for dozens of users per day
* Worldwide for hundreds of users per day and large data serving requirements


E9\. Update the code in `coffeeApp/app.R` so that instead of centering on Brazil the user can select which country to focus on:


* Using `[textInput()](https://rdrr.io/pkg/shiny/man/textInput.html)`
* Using `[selectInput()](https://rdrr.io/pkg/shiny/man/selectInput.html)`


E10\. Reproduce Figure 9\.1 and Figure 9\.7 as closely as possible using the **ggplot2** package.


E11\. Join `us_states` and `us_states_df` together and calculate a poverty rate for each state using the new dataset.
Next, construct a continuous area cartogram based on total population.
Finally, create and compare two maps of the poverty rate: (1\) a standard choropleth map and (2\) a map using the created cartogram boundaries.
What is the information provided by the first and the second map?
How do they differ from each other?


E12\. Visualize population growth in Africa.
Next, compare it with the maps of a hexagonal and regular grid created using the **geogrid** package.





[8 Geographic data I/O](/read-write)
[10 Bridges to GIS software](/gis)

Second Edition
--------------



* [Visit the geocompx website 🌐](https://geocompx.org/)
* [Install updated packages 💾](https://r.geocompx.org/#reproducibility)
* [Open an issue](https://github.com/geocompx/geocompr/issues)
* [Chat on Discord](https://discord.gg/PMztXYgNxp)
* [Check exercise solutions](https://r.geocompx.org/solutions/)
* [Support Ukraine 🇺🇦](https://supportukrainenow.org/)




---


On this page
------------


* [9 Making maps with R](#adv-map)
* [Prerequisites](#prerequisites-7)
* [9\.1 Introduction](#introduction-5)
* [9\.2 Static maps](#static-maps)
	+ [9\.2\.1 tmap basics](#tmap-basics)
	+ [9\.2\.2 Map objects](#map-obj)
	+ [9\.2\.3 Visual variables](#visual-variables)
	+ [9\.2\.4 Scales](#scales)
	+ [9\.2\.5 Legends](#legends)
	+ [9\.2\.6 Layouts](#layouts)
	+ [9\.2\.7 Faceted maps](#faceted-maps)
	+ [9\.2\.8 Inset maps](#inset-maps)
* [9\.3 Animated maps](#animated-maps)
* [9\.4 Interactive maps](#interactive-maps)
* [9\.5 Mapping applications](#mapping-applications)
* [9\.6 Other mapping packages](#other-mapping-packages)
* [9\.7 Exercises](#exercises-7)



* [View source](https://github.com/geocompx/geocompr/blob/main/09-mapping.Rmd)
* [Edit this page](https://github.com/geocompx/geocompr/edit/main/09-mapping.Rmd)






 


"**Geocomputation with R**" was written by Robin Lovelace, Jakub Nowosad, Jannes Muenchow. It was last built on 2024\-10\-19\.




This book was built by the [bookdown](https://bookdown.org) R package.








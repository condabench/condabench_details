






Data Package Containing Information About Elevators in NYC • elevators
















[Skip to contents](#main)

[elevators](index.html)
0\.0\.0\.9000




* [Reference](reference/index.html)





* 








elevators
=========





This data package contains a data set of the registered elevator devices in New York City provided by the Department of Buildings in response to a September 2015 FOIL request.



Installation
------------


You can install the development version of elevators like so:



```

remotes::install_github("emilhvitfeldt/elevators")
```



Examples
--------


One of the fundamental characteristics about elevators is how fast they can go, and how much they can carry



```

[library](https://rdrr.io/r/base/library.html)([elevators](https://github.com/EmilHvitfeldt/elevators))
[library](https://rdrr.io/r/base/library.html)([ggplot2](https://ggplot2.tidyverse.org))

elevators |>
  ggplot(aes(speed_fpm, capacity_lbs)) +
  geom_point(alpha = 0.1)
```

![](opensource/tidytuesday/2022-12-06/images/0.png)


In addition to `borough`, there are a number of geographical variables can would be useful to explore



```

elevators |>
  ggplot(aes(longitude, latitude, color = borough)) +
  coord_map() +
  geom_point(alpha = 0.1) +
  theme_minimal()
```

![](opensource/tidytuesday/2022-12-06/images/1.png)


We can also see where the different tall buildings are in Manhattan



```

[library](https://rdrr.io/r/base/library.html)([tidyverse](https://tidyverse.tidyverse.org))

elevators |>
  [filter](https://rdrr.io/r/stats/filter.html)(borough == "Manhattan") |>
  mutate(floors = str_extract(floor_to, "\\d+"),
         floors = [as.numeric](https://rdrr.io/r/base/numeric.html)(floors)) |>
  [filter](https://rdrr.io/r/stats/filter.html)(![is.na](https://rdrr.io/r/base/NA.html)(floors), floors < 100, floors > 0) |>
  ggplot(aes(longitude, latitude, color = floors)) +
  geom_point(alpha = 0.05) +
  scale_color_viridis_c() +
  theme_minimal() +
  facet_wrap(~ cut_width(floors, width = 10, boundary = 0))
```

![](opensource/tidytuesday/2022-12-06/images/2.png)





Links
-----


* [Browse source code](https://github.com/EmilHvitfeldt/elevators/)
* [Report a bug](https://github.com/EmilHvitfeldt/elevators/issues)




License
-------


* [Full license](LICENSE.html)
* [MIT](https://opensource.org/licenses/mit-license.php) \+ file [LICENSE](LICENSE-text.html)




Citation
--------


* [Citing elevators](authors.html#citation)




Developers
----------


* Emil Hvitfeldt   
 Author, maintainer







Developed by Emil Hvitfeldt.





Site built with [pkgdown](https://pkgdown.r-lib.org/) 2\.0\.6\.








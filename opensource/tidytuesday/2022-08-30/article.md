






Introduction to pell • pell
















[Skip to contents](#main)

[pell](../index.html)
0\.1\.0




* [Get started](../articles/intro.html)
* [Reference](../reference/index.html)
* [Articles](#)

###### Use pell


[Examples using ggplot2](../articles/examples.html)

###### Extras


[Download the data directly](../articles/download.html)
* [Changelog](../news/index.html)





* 







Introduction to pell
====================


Source: [`vignettes/intro.Rmd`](https://github.com/Curious-Joe/pell/blob/HEAD/vignettes/intro.Rmd)
`intro.Rmd`



---


The `pell` R package contains one dataset that provides
data about pell award distribution by the universities/colleges across
the United States since 1999 to 2017\. This introductory vignette
provides some overall statistics and visualization about the data to
inspire potential use of this data.




Installation
------------


You can install the released version of `pell` from [CRAN](https://CRAN.R-project.org) with:



```

[install.packages](https://rdrr.io/r/utils/install.packages.html)("pell")
```

Or install the development version from [GitHub](https://github.com/) with:



```

[install.packages](https://rdrr.io/r/utils/install.packages.html)("devtools")
devtools::install_github("Curious-Joe/pell")
```



The **pell** package
--------------------


This package contains one dataset called \- pell. Take a glimpse at
the data:



```

dplyr::[glimpse](https://pillar.r-lib.org/reference/glimpse.html)(pell)
#> Rows: 100,474
#> Columns: 6
#> $ STATE     <fct> AK, AK, AK, AK, AK, AK, AL, AL, AL, AL, AL, AL, AL, AL, AL, …
#> $ AWARD     <dbl> 197232.9, 133148.0, 107287.0, 3425148.8, 2441864.0, 353170.0…
#> $ RECIPIENT <dbl> 109, 69, 72, 1920, 1256, 221, 2369, 837, 3236, 854, 2842, 16…
#> $ NAME      <fct> "Alaska Pacific University", "Alaska Vocational Technical Ce…
#> $ SESSION   <fct> 1999-00, 1999-00, 1999-00, 1999-00, 1999-00, 1999-00, 1999-0…
#> $ YEAR      <int> 1999, 1999, 1999, 1999, 1999, 1999, 1999, 1999, 1999, 1999, …
```

The `[pell::pell](../reference/pell.html)` data contains 100470 complete cases, with
4 missing values.



```

visdat::[vis_dat](https://docs.ropensci.org/visdat/reference/vis_dat.html)(pell)
```




Highlights
----------


Without going much into the details, here are few code snippet to get
you started with the `pell` dataset. You can check out more
in `[vignette("examples")](../articles/examples.html)`.



### Exploring factors


The `pell` data has three factor variables:



```

pell %>%
  dplyr::[select](https://dplyr.tidyverse.org/reference/select.html)(where(is.factor)) %>% 
  dplyr::[glimpse](https://pillar.r-lib.org/reference/glimpse.html)()
#> Rows: 100,474
#> Columns: 3
#> $ STATE   <fct> AK, AK, AK, AK, AK, AK, AL, AL, AL, AL, AL, AL, AL, AL, AL, AL…
#> $ NAME    <fct> "Alaska Pacific University", "Alaska Vocational Technical Cent…
#> $ SESSION <fct> 1999-00, 1999-00, 1999-00, 1999-00, 1999-00, 1999-00, 1999-00,…
```

Get the top 10 states with the highest median Pell grant record:



```

# Top 10 institutions with the highest pell grant disbursements
pell %>%
  dplyr::[group_by](https://dplyr.tidyverse.org/reference/group_by.html)(STATE) %>%
  dplyr::[summarise](https://dplyr.tidyverse.org/reference/summarise.html)(
    Median = [median](https://rdrr.io/r/stats/median.html)(.data$AWARD, na.rm = TRUE)
  ) %>%
  dplyr::[arrange](https://dplyr.tidyverse.org/reference/arrange.html)(desc(Median)) %>%
  [head](https://rdrr.io/r/utils/head.html)(10) %>%
  knitr::[kable](https://rdrr.io/pkg/knitr/man/kable.html)(caption = "Top 10 States with the Highest Median Grant Distribution")
```



Top 10 States with the Highest Median Grant
Distribution
| STATE | Median |
| --- | --- |
| FM | 8787878 |
| AS | 4181457 |
| AL | 3067752 |
| MS | 2989801 |
| MH | 2826818 |
| GU | 2706895 |
| VI | 2388619 |
| PW | 2206829 |
| NC | 2113618 |
| MP | 1920043 |


Get a treemap of all the states based on their total paid out grant
dollars:



```

treemap::[treemap](https://rdrr.io/pkg/treemap/man/treemap.html)(pell,
            index=[c](https://rdrr.io/r/base/c.html)("STATE"),
            vSize="AWARD",
            type="index",
            
            ) 
```




### More


If you are a Python user, you may find interest in checking a [dash app](https://plotly.com/dash/) that I created earlier
using the same data. Check out the app repository [here](https://github.com/Curious-Joe/Pell-Awardees-in-US-Colleges).






I will try to put some more R examples in
`[vignette("examples")](../articles/examples.html)` but currently it’s not populated.


So keep an eye on that or do you own analysis and contribute your
own!





Package citation
----------------


Please cite the `pell` R package using:



```

[citation](https://rdrr.io/r/utils/citation.html)("pell")
#> To cite package 'pell' in publications use:
#> 
#>   Hossain A (2023). _pell: Data About Historic Pell Grant Distribution
#>   in the US_. https://github.com/Curious-Joe/pell,
#>   https://curious-joe.github.io/pell/.
#> 
#> A BibTeX entry for LaTeX users is
#> 
#>   @Manual{,
#>     title = {pell: Data About Historic Pell Grant Distribution in the US},
#>     author = {Arafath Hossain},
#>     year = {2023},
#>     note = {https://github.com/Curious-Joe/pell,
#> https://curious-joe.github.io/pell/},
#>   }
```

Have fun with the pell grant data!




---


Thanks to the [`palmerpenguins`](https://github.com/allisonhorst/palmerpenguins)
package for their great vignette. I used the vignette from that package
as a skeleton and populated this vignette with relevant contents. A big
shout out to them and a heartfelt thank you 🙏



On this page
------------






Developed by Arafath Hossain.





Site built with [pkgdown](https://pkgdown.r-lib.org/) 2\.0\.7\.








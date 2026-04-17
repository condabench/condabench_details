





TidyTuesday Dataset Metadata • ttmeta









[Skip to contents](#main)

[ttmeta](index.html)
0\.1\.0\.20241028




* [Reference](reference/index.html)


* 
* 







ttmeta
======



Metadata about the [TidyTuesday](https://tidytues.day) social data project. Data includes a summary of each weekly TidyTuesday post, information about the articles and data sources linked in those posts, and details about the datasets themselves, including variable names and classes.


The package updates weekly with the latest TidyTuesday data. Note that the package version does *not* automatically change (yet) during that update, so the date in the version number currently reflects the last time the data was *manually* parsed.



Installation
------------


You can install the development version of ttmeta from [GitHub](https://github.com/) with:



```

# install.packages("pak")
pak::[pak](https://pak.r-lib.org/reference/pak.html)("r4ds/ttmeta")
```



Usage
-----


The useful parts of this package are the three exported datasets:


* `tt_summary_tbl` contains a summary of the weekly TidyTuesday posts.
* `tt_urls_tbl` contains source and article urls for TidyTuesday posts.
* `tt_datasets_metadata` contains metadata about the weekly TidyTuesday datasets.




Code of Conduct
---------------


Please note that the ttmeta project is released with a [Contributor Code of Conduct](https://r4ds.github.io/ttmeta/CODE_OF_CONDUCT.html). By contributing to this project, you agree to abide by its terms.





Links
-----


* [Browse source code](https://github.com/r4ds/ttmeta/)
* [Report a bug](https://github.com/r4ds/ttmeta/issues)




License
-------


* [Full license](LICENSE.html)
* [MIT](https://opensource.org/licenses/mit-license.php) \+ file [LICENSE](LICENSE-text.html)




Community
---------


* [Contributing guide](CONTRIBUTING.html)
* [Code of conduct](CODE_OF_CONDUCT.html)
* [Getting help](SUPPORT.html)




Citation
--------


* [Citing ttmeta](authors.html#citation)




Developers
----------


* Jon Harmon   
 Author, maintainer




Dev status
----------


* 
* 
* 
* 






Developed by Jon Harmon.




Site built with [pkgdown](https://pkgdown.r-lib.org/) 2\.1\.1\.








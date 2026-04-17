





Network Visualizations of Code Collections (funspotr part 3\) \- Bryan Shalloway's Blog

















* [About](/about/)
* [Presentations](https://www.youtube.com/watch?v=c9oU7ALJS3o&list=PL2f6B79nBqL16QFte8fN_GWDtJwZDXt95&index=1)
* [GitHub](https://github.com/brshallo)
* [LinkedIn](https://www.linkedin.com/in/bryanshalloway/)
* [Twitter](https://twitter.com/brshallo)






Network Visualizations of Code Collections (funspotr part 3\)
=============================================================



 
 
 Tags:
 
 [dplyr](/tags/dplyr)
[funspotr](/tags/funspotr)
[readr](/tags/readr)



2022\-03\-17


Show/Hide all code


* [Show All Code](#)
* [Hide All Code](#)















* [Interactive network plots](#interactive-network-plots)
	+ [Julia Silge Blog](#julia-silge-blog)
	+ [David Robinson Tidy Tuesday](#david-robinson-tidy-tuesday)
	+ [R for Data Science Chapters](#r-for-data-science-chapters)
	+ [My blog](#my-blog)
	+ [My gists](#my-gists)



In previous posts and threads I’ve alluded to the potential utility of visualizing the relationships between parsed functions/packages and files as a network plot.



> It can be helpful to review the relationship between your [\#rstats](https://twitter.com/hashtag/rstats?src=hash&ref_src=twsrc%5Etfw) code files by looking at a network graph of them by packages loaded.  
>   
> Graph of 50\+ of my gists (squares) and packages (circles) used.  
>   
> That node at the center is {dplyr}. [pic.twitter.com/XmNxOrgDtF](https://t.co/XmNxOrgDtF)
> 
> 
> 
> — Bryan Shalloway (@brshallo) [March 16, 2022](https://twitter.com/brshallo/status/1503905135692374018?ref_src=twsrc%5Etfw)



I added the function `network_plot()` to [funspotr](https://github.com/brshallo/funspotr). In this post I’ll simply output the network plots of the parsed\-out packages from the code collections discussed in the prior two posts:


* [Identifying R Functions \& Packages Used in GitHub Repos (funspotr part 1\)](https://www.bryanshalloway.com/2022/01/18/identifying-r-functions-packages-used-in-github-repos/)
* [Identifying R Functions \& Packages in Github Gists (funspotr part 2\)](https://www.bryanshalloway.com/2022/02/07/identifying-r-functions-packages-in-your-github-gists/)



```
library(dplyr)
library(funspotr)
```


Interactive network plots
=========================


The network plots show files as squares and packages as circles, edges represent cases where a package is used in a given file[1](#fn1).



Julia Silge Blog
----------------



```
readr::read_csv("https://raw.githubusercontent.com/brshallo/funspotr-examples/main/data/funs/jsilge-blog-funs-20220114.csv") %>% 
  # not including base R or any custom functions or packages I don't have installed
  filter(!is.na(pkgs), !(pkgs %in% c("base", "(unknown)"))) %>% 
  network_plot(to = pkgs)
```



* tidymodels and tidyverse packages are both central to Julia’s posts. The cluster of tidymodels packages show\-up (for the most part) just to the right of the cluster of core tidyverse packages.




David Robinson Tidy Tuesday
---------------------------



```
readr::read_csv("https://raw.githubusercontent.com/brshallo/funspotr-examples/main/data/funs/drob-tidy-tuesdays-funs-20220114.csv") %>% 
  filter(!is.na(pkgs), !(pkgs %in% c("base", "(unknown)"))) %>% 
  network_plot(to = pkgs)
```



* Similar to Julia’s posts, tidyverse packages are central to David’s Tidy Tuesday files.. However the tidymodels packages are less central and can be seen in a cluster at the bottom of the plot.
* In both plots we see {broom} not showing\-up by the other tidymodels packages. This is unsurprising for while broom is in the tidymodels ecosystem it has many common uses outside of predictive modeling and has a longer legacy than most tidymodels packages.




R for Data Science Chapters
---------------------------



```
readr::read_csv("https://raw.githubusercontent.com/brshallo/funspotr-examples/main/data/funs/r4ds-chapter-files-funs-20220117.csv") %>% 
  filter(!is.na(pkgs), !(pkgs %in% c("base", "(unknown)"))) %>% 
  network_plot(to = pkgs)
```





My blog
-------



```
readr::read_csv("https://raw.githubusercontent.com/brshallo/funspotr-examples/main/data/funs/brshallo-blog-funs-20220114.csv") %>% 
  filter(!is.na(pkgs), !(pkgs %in% c("base", "(unknown)"))) %>% 
  network_plot(to = pkgs)
```





My gists
--------



```
readr::read_csv("https://raw.githubusercontent.com/brshallo/brshallo/master/content/post/2022-02-07-identifying-r-functions-packages-in-your-github-gists/data/brshallo-gists-20220314.csv") %>% 
  filter(!is.na(pkgs), !(pkgs %in% c("base", "(unknown)"))) %>% 
  network_plot(to = pkgs)
```



* This figure is a bit different than the graph shown in my tweet above as it includes more of my gists and uses a different algorithm to construct the network.
* dplyr, purrr, and tidyr are the three packages at the center







---


1. With all of these I think more time could go into tailoring the network plot. It would also be interesting to look into measures of network relatedness between the files… maybe in a future post…[↩︎](#fnref1)








Please enable JavaScript to view the [comments powered by Disqus.](https://disqus.com/?ref_noscript)



* [Tags](/tags)
* [Categories](/categories)
* [RSS feed](/index.xml)
* Blogroll:[R\-Bloggers](https://www.r-bloggers.com/)[R\-Weekly](https://rweekly.org/)















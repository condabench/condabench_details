Scraping Gdpr Fines \- Roel's R\-tefacts
Toggle navigation

[Roel's R\-tefacts](https://blog.rmhogervorst.nl)* [Blog](/ "Blog")
* [About](/about/ "About")
* [Getting updates](/subscribing "Getting updates")
* [search and more](/search_and_more/ "search and more ")




Scraping Gdpr Fines
===================

Into the DOM with a flavour of regex
------------------------------------

 Posted on April 8, 2020
  (Last modified on November 9, 2022\)
 \|  4 minutes
 \|  774 words
 \|  [Roel M. Hogervorst](https://rmhogervorst.nl)The website Privacy Affairs keeps a list of fines related to GDPR.
I heard \* that this might be an interesting dataset for TidyTuesdays and so I scraped it. The dataset contains at this
moment 250 fines given out for GDPR violations and is last updated (according to the website) on 31 March 2020\.


> All data is from official government sources, such as official reports of national Data Protection Authorities.

The largest fine is €50,000,000 on Google Inc. on January 21 , 2019 \- in France, and the smallest is actually 0 euros, but the website says 90\.

cover image

Scraping
========

I use the {rvest} package to scrape the website.

Before you start
----------------

I first checked the [robots.txt](https://www.privacyaffairs.com/robots.txt) of this website. And it
did not disallow me to scrape the website.

The scraping
============

I thought this would be easy and done in a minute. But there were some snafus.
It works for now, but if the website changes a bit this scraping routine will not work that well anymore. It extracts the script part of the website and extracts the data between ‘\[’ and ’]’.
If anyone has ideas on making this more robust, be sure to let me know over twitter.

Details about the scraping part
-------------------------------

First I noticed that the website doesn’t show you all of the fines. But when we look at the source of the page it seems they are all there. It should be relatively simple to retrieve the data, the data is
in the javaScript part (see picture).


!!!! I received an update from two twitter peeps on how to simplify the extraction, using rvest and V8\. See the github link <https://github.com/RMHogervorst/scrape_gdpr_fines>. !!!

But extracting that data is quite some more work:

* First find the \< script \> tag on the website
* Find the node that contains the data
* Realize that there are actually two datasources in here


```
library(rvest)
```

```
link<- "https://www.privacyaffairs.com/gdpr-fines/"
page <- read_html(link)


temp <- page %>% html_nodes("script") %>% .[9] %>% 
  rvest::html_text() 
```
* cry (joking, don’t give up! The \#rstats community will help you!)
* do some advanced string manipulation to extract the two json structures
* Read the json data in R


```
ends <- str_locate_all(temp, "\\]")
starts <- str_locate_all(temp, "\\[")
table1 <- temp %>% stringi::stri_sub(from = starts[[1]][1,2], to = ends[[1]][1,1]) %>% 
  str_remove_all("\n") %>% 
  str_remove_all("\r") %>%
  jsonlite::fromJSON()

table2 <- temp %>% stringi::stri_sub(from = starts[[1]][2,2], to = ends[[1]][2,1]) %>% 
  str_remove_all("\n") %>% 
  str_remove_all("\r") %>%  
  jsonlite::fromJSON()
```
* Profit

I also tried it in pure text before I gave up and returned to html parsing. You can see that in the repo.

(\*) I was tricked through twitter \#rstats on \#tidytuesday


<https://twitter.com/hrbrmstr/status/1247476867621421061>

Links
-----

* RVEST Documentation [https://rvest.tidyverse.org/articles/harvesting\-the\-web.html\#css\-selectors](https://rvest.tidyverse.org/articles/harvesting-the-web.html#css-selectors)
* The source website for the data set [https://www.privacyaffairs.com/gdpr\-fines/](https://www.privacyaffairs.com/gdpr-fines/)
* Tidy Tuesday website <https://github.com/rfordatascience/tidytuesday>
* Sourcecode for the scraper <https://github.com/RMHogervorst/scrape_gdpr_fines>
* Picture credit: Photo by Paulius Dragunas on Unsplash <https://unsplash.com/photos/uw_NWjC1mBE>

### State of the machine

At the moment of creation (when I knitted this document ) this was the state of my machine: **click here to expand**
```
sessioninfo::session_info()
```

```
## ─ Session info ───────────────────────────────────────────────────────────────
##  setting  value
##  version  R version 4.2.0 (2022-04-22)
##  os       macOS Big Sur/Monterey 10.16
##  system   x86_64, darwin17.0
##  ui       X11
##  language (EN)
##  collate  en_US.UTF-8
##  ctype    en_US.UTF-8
##  tz       Europe/Amsterdam
##  date     2022-11-09
##  pandoc   2.18 @ /Applications/RStudio.app/Contents/MacOS/quarto/bin/tools/ (via rmarkdown)
## 
## ─ Packages ───────────────────────────────────────────────────────────────────
##  package     * version date (UTC) lib source
##  blogdown      1.10    2022-05-10 [1] CRAN (R 4.2.0)
##  bookdown      0.27    2022-06-14 [1] CRAN (R 4.2.0)
##  bslib         0.4.0   2022-07-16 [1] CRAN (R 4.2.0)
##  cachem        1.0.6   2021-08-19 [1] CRAN (R 4.2.0)
##  cli           3.3.0   2022-04-25 [1] CRAN (R 4.2.0)
##  digest        0.6.29  2021-12-01 [1] CRAN (R 4.2.0)
##  evaluate      0.15    2022-02-18 [1] CRAN (R 4.2.0)
##  fastmap       1.1.0   2021-01-25 [1] CRAN (R 4.2.0)
##  htmltools     0.5.3   2022-07-18 [1] CRAN (R 4.2.0)
##  httr          1.4.3   2022-05-04 [1] CRAN (R 4.2.0)
##  jquerylib     0.1.4   2021-04-26 [1] CRAN (R 4.2.0)
##  jsonlite      1.8.0   2022-02-22 [1] CRAN (R 4.2.0)
##  knitr         1.39    2022-04-26 [1] CRAN (R 4.2.0)
##  lifecycle     1.0.1   2021-09-24 [1] CRAN (R 4.2.0)
##  magrittr      2.0.3   2022-03-30 [1] CRAN (R 4.2.0)
##  R6            2.5.1   2021-08-19 [1] CRAN (R 4.2.0)
##  rlang         1.0.6   2022-09-24 [1] CRAN (R 4.2.0)
##  rmarkdown     2.14    2022-04-25 [1] CRAN (R 4.2.0)
##  rstudioapi    0.13    2020-11-12 [1] CRAN (R 4.2.0)
##  rvest       * 1.0.2   2021-10-16 [1] CRAN (R 4.2.0)
##  sass          0.4.2   2022-07-16 [1] CRAN (R 4.2.0)
##  sessioninfo   1.2.2   2021-12-06 [1] CRAN (R 4.2.0)
##  stringi       1.7.8   2022-07-11 [1] CRAN (R 4.2.0)
##  stringr       1.4.1   2022-08-20 [1] CRAN (R 4.2.0)
##  xfun          0.31    2022-05-10 [1] CRAN (R 4.2.0)
##  xml2          1.3.3   2021-11-30 [1] CRAN (R 4.2.0)
##  yaml          2.3.5   2022-02-21 [1] CRAN (R 4.2.0)
## 
##  [1] /Library/Frameworks/R.framework/Versions/4.2/Resources/library
## 
## ──────────────────────────────────────────────────────────────────────────────
```


---

[Scraping Gdpr Fines](https://blog.rmhogervorst.nl/blog/2020/04/08/scraping-gdpr-fines/)Posted on April 8, 2020
by
 \|  [Roel M. Hogervorst](https://rmhogervorst.nl)[rvest](https://blog.rmhogervorst.nltags/rvest/) 
[GDPR](https://blog.rmhogervorst.nltags/gdpr/) 
[privacy](https://blog.rmhogervorst.nltags/privacy/) 
[short](https://blog.rmhogervorst.nltags/short/) 
[scraping](https://blog.rmhogervorst.nltags/scraping/) More posts of level:
[intermediate](https://blog.rmhogervorst.nl/difficulty/intermediate/) #### See also

* [Downloading files from a webserver, and failing.](/blog/2017/12/08/downloading-multiple-files-and-failing/)
* [← Previous Post](https://blog.rmhogervorst.nl/blog/2019/10/11/gosset-part-2-small-sample-statistics/ "Gosset part 2: small sample statistics")
* [Next Post →](https://blog.rmhogervorst.nl/blog/2020/04/14/where-does-the-output-of-rscript-go/ "Where does the output of Rscript go?")










[Roel M. Hogervorst](rmhogervorst.nl)
 • 
2024
 • 
[Roel's R\-tefacts](https://blog.rmhogervorst.nl)
Donate using Liberapay or buy me a coffee 

[Hugo v0\.82\.0](https://gohugo.io) powered  •  Theme [Beautiful Hugo](https://github.com/halogenica/beautifulhugo) adapted from [Beautiful Jekyll](https://deanattali.com/beautiful-jekyll/)  
See anything wrong? Click to add them to [the issue tracker](https://github.com/RMHogervorst/blog/issues)  
[or edit this page on github.](https://github.com/RMHogervorst/blog/tree/master/content/post/2020-04-08-scraping-gdpr-fines.Rmd)


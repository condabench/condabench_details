



Introducing ravelRy, a new R package!























































Close

Menu


* [Home](https://www.kaylinpavlik.com/)
* [About](https://www.kaylinpavlik.com/about/)
* [Twitter](https://twitter.com/kaylinquest "@kaylinquest")
* [Subscribe](https://www.kaylinpavlik.com/rss/)













 [Home](https://www.kaylinpavlik.com "Home")


Menu


Introducing ravelRy, a new R package!
=====================================


[Kaylin Pavlik](/author/walkerkq/) \| 12 Jan 2020 \| 4 min read






Introducing my first R package, [**ravelRy**](https://github.com/walkerkq/ravelRy?ref=kaylinpavlik.com)! 



*Background image by [Paul Hanaoka](https://unsplash.com/@paul_?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) via [Unsplash](https://unsplash.com/s/photos/yarn?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*

[**ravelRy**](https://github.com/walkerkq/ravelRy?ref=kaylinpavlik.com) is an R wrapper for the [Ravelry.com API](https://www.ravelry.com/groups/ravelry-api?ref=kaylinpavlik.com). Ravelry describes itself as a social networking and organizational tool for knitters, crocheters, designers, spinners, weavers and dyers. 

The API provides access to knit and crochet patterns and their attributes (such as ratings, yarn type, needle type, price, photos, and author/designer info), yarn data (like brand, ratings, texture, price, yardage, and fiber type), author information, shop locations, and more. 



A knitting pattern on Ravelry: [Jason's Cashmere Hat](https://www.ravelry.com/patterns/library/jasons-cashmere-hat?ref=kaylinpavlik.com)

Getting set up
--------------

First, download the package. You can either download from CRAN or from the development version on Github.  


```
install.packages("ravelRy")

devtools::install_github("walkerkq/ravelRy")

```
### Authenticating

To access the API, you'll need a free developer account, which you can create at [https://www.ravelry.com/pro/developer](https://www.ravelry.com/pro/developer?ref=kaylinpavlik.com). Then, create an app with basic read only authentication to receive a username and password. 

You can either set the environment variables `RAVELRY_USERNAME` and `RAVELRY_PASSWORD` in your .Renviron file, or via the R console using the `ravelry_auth` function. 


```
ravelry_auth(key = 'username') # you will be prompted to enter your username 
ravelry_auth(key = 'password') # you will be prompted to enter your password 
```
### Retrieving data

You can search for patterns using the function `search_patterns`:


```
search_results <- search_patterns(query = 'hat', page_size = 5, availability = 'free', fit = 'baby')
str(search_results, max.level = 1)

Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	2 obs. of  7 variables:
 $ free            : logi  TRUE TRUE
 $ id              : int  124400 464893
 $ name            : chr  "Sockhead Slouch Hat" "Garter Ear Flap Hat"
 $ permalink       : chr  "sockhead-slouch-hat" "garter-ear-flap-hat"
 $ designer.id     : int  21767 40686
 $ designer.name   : chr  "Kelly McClure" "Purl Soho"
 $ pattern_sources : List of 2
```
And pull pattern data using the returned pattern `id`s: 


```
patterns <- get_patterns(ids = search_results$id)
str(patterns, max.level = 1)

'data.frame':	2 obs. of  50 variables:
 $ comments_count          : int  89 156
 $ created_at              : chr  "2014/01/23 11:39:14 -0500" "2009/05/25 16:17:05 -0400"
 $ currency                : chr  "USD" ""
 $ difficulty_average      : num  2.41 1.52
 $ difficulty_count        : int  2452 4897
 $ downloadable            : logi  TRUE TRUE
 $ favorites_count         : int  45850 43980
 $ free                    : logi  TRUE TRUE
 $ gauge                   : num  4.25 32
 $ gauge_divisor           : int  1 4
 $ gauge_pattern           : chr  "garter stitch" "stockinette stitch  "
 $ generally_available     : chr  "2014/01/01 00:00:00 -0500" "2009/05/01 00:00:00 -0400"
 $ id                      : int  464893 124400
 $ name                    : chr  "Garter Ear Flap Hat" "Sockhead Slouch Hat"
 $ pdf_url                 : chr  "https://www.purlsoho.com/create/wp-content/uploads/2014/01/Purl_Bee_Garter_Ear_Flap_Hats.pdf" ""
 $ permalink               : chr  "garter-ear-flap-hat" "sockhead-slouch-hat"
 $ price                   : chr  "" ""
 $ projects_count          : int  9831 21702
 $ published               : chr  "2014/01/01" "2009/05/01"
 $ queued_projects_count   : int  6969 8867
 $ rating_average          : num  4.62 4.65
 $ rating_count            : int  2479 4787
 $ row_gauge               : num  8 46
 $ updated_at              : chr  "2019/04/18 14:10:08 -0400" "2019/12/03 18:34:33 -0500"
 $ url                     : chr  "https://www.purlsoho.com/create/2014/01/23/lauras-loop-garter-ear-flap-hat/" "http://bohoknits.blogspot.com/2009/05/sockhead-hat.html"
 $ yardage                 : int  60 155
 $ yardage_max             : int  160 415
 $ personal_attributes     : chr  "" ""
 $ sizes_available         : chr  "Baby, Toddler, Kid, Adult Small, Adult Medium, Adult Large" "baby, child, teen, adult small, medium, large, extra-large"
 $ product_id              : chr  "" "19200"
 $ currency_symbol         : chr  "$" ""
 $ ravelry_download        : logi  FALSE TRUE
 $ download_location       : List of 2
 $ pdf_in_library          : logi  FALSE FALSE
 $ volumes_in_library      : chr  "" ""
 $ gauge_description       : chr  "4.25 stitches and 8 rows = 1 inch in garter stitch" "32 stitches and 46 rows = 4 inches in stockinette stitch  "
 $ yarn_weight_description : chr  "Aran (8 wpi)" "Fingering (14 wpi)"
 $ yardage_description     : chr  "60 - 160 yards" "155 - 415 yards"
 $ pattern_needle_sizes    : List of 2
 $ notes_html              : chr  "\n<p>MATERIALS</p>\n\n<ul>\n<li>1 (1, 1, 1, 2, 2) skein(s) of Purl Soho’s Alpaca Pure, 100% alpaca. We used the"| __truncated__ 
 $ notes                   : chr  "MATERIALS\r\n\r\n- 1 (1, 1, 1, 2, 2) skein(s) of Purl Soho's Alpaca Pure, 100% alpaca. We used the colors Heirl"| __truncated__ 
 $ packs                   : List of 2
 $ printings               : List of 2
 $ yarn_weight             : List of 2
 $ craft                   : List of 2
 $ pattern_categories      : List of 2
 $ pattern_attributes      : List of 2
 $ pattern_author          : List of 2
 $ photos                  : List of 2
 $ pattern_type            : List of 2
```
Or search for yarn: 


```
yarn_results <- search_yarn(query = 'wool', page_size = 2, sort = 'rating')
str(yarn_results, max.level = 1)

Classes ‘tbl_df’, ‘tbl’ and 'data.frame':	2 obs. of  17 variables:
 $ discontinued      : logi  FALSE FALSE
 $ gauge_divisor     : chr  "" ""
 $ grams             : int  100 115
 $ id                : int  166904 49035
 $ machine_washable  : chr  "" ""
 $ max_gauge         : chr  "" ""
 $ min_gauge         : chr  "" ""
 $ name              : chr  "Cashmere Sock" "Fiber"
 $ permalink         : chr  "the-wool-barn-cashmere-sock" "hello-yarn-fiber"
 $ rating_average    : num  5 5
 $ rating_count      : int  46 41
 $ rating_total      : int  230 205
 $ texture           : chr  "" ""
 $ thread_size       : chr  "" ""
 $ wpi               : chr  "" ""
 $ yardage           : chr  "382" ""
 $ yarn_company_name : chr  "The Wool Barn" "Hello Yarn"
```
And return yarn attributes: 


```
yarn_details <- get_yarns(ids = yarn_results$id)
str(yarn_details, max.level = 1)

'data.frame':	2 obs. of  26 variables:
 $ discontinued        : logi  FALSE FALSE
 $ gauge_divisor       : chr  "" ""
 $ grams               : int  100 115
 $ id                  : int  166904 49035
 $ machine_washable    : chr  "" ""
 $ max_gauge           : chr  "" ""
 $ min_gauge           : chr  "" ""
 $ name                : chr  "Cashmere Sock" "Fiber"
 $ permalink           : chr  "the-wool-barn-cashmere-sock" "hello-yarn-fiber"
 $ rating_average      : num  5 5
 $ rating_count        : int  46 41
 $ rating_total        : int  230 205
 $ texture             : chr  "" ""
 $ thread_size         : chr  "" ""
 $ wpi                 : chr  "" ""
 $ yardage             : chr  "382" ""
 $ notes_html          : chr  "" "\n<p>Hand-dyed spinning fiber from <a href=\"http://shop.helloyarn.com/\">Hello Yarn</a>.</p>\n"
 $ min_needle_size     : List of 2
 $ max_needle_size     : List of 2
 $ min_hook_size       : chr  "" ""
 $ max_hook_size       : chr  "" ""
 $ personal_attributes : chr  "" ""
 $ yarn_company        : List of 2
 $ yarn_fibers         : List of 2
 $ photos              : List of 2
 $ yarn_weight         : List of 2
```
Happy data exploring! 





Share:
[Twitter](https://twitter.com/share?text=Introducing ravelRy, a new R package!&url=https://www.kaylinpavlik.com/introducing-new-r-package-ravelry/)
[Facebook](https://www.facebook.com/sharer/sharer.php?u=https://www.kaylinpavlik.com/introducing-new-r-package-ravelry/)


Tags:
[R](/tag/r/) [package](/tag/package/) [crochet](/tag/crochet/) [knitting](/tag/knitting/) [api wrapper](/tag/api-wrapper/)







#### [Kaylin Pavlik](/author/walkerkq/)


Data scientist • walkerkq2@gmail.com • github.com/walkerkq 


 Minneapolis, MN
 [Twitter](https://twitter.com/kaylinquest)





Show Comments



[How do fiber types appear together in yarn blends? \[R \+ ravelRy]
------------------------------------------------------------------


Using yarn data pulled via ravelRy, this post explores how different types of fibers appear together in popular yarn blends.…](/ravelry-yarn-fibers/)
[Understanding \+ classifying genres using Spotify audio features
----------------------------------------------------------------


Musical genre is far from black and white \- there are no hard and fast rules for classifying a given track or artist as “hard rock” vs. “folk rock,” but rather the listener knows it when they hear it. Is it possible to classify songs into broad genres?…](/classifying-songs-genres/)









Theme [Attila](https://github.com/zutrinken/attila) by [zutrinken](https://zutrinken.com)
Published with [Ghost](https://ghost.org)








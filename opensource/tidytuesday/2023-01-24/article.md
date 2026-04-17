








Alone R package: Datasets from the survival TV series \- Dan Oehm \| Gradient Descending







































































Toggle navigation




[Dan Oehm \| Gradient Descending](https://gradientdescending.com/)
==================================================================

 
* [Blog](# "Blog") 
	+ [All](http://gradientdescending.com "All")
	+ [R](https://gradientdescending.com/category/r/ "R")
	+ [Tidy Tuesday](https://gradientdescending.com/category/tidy-tuesday/ "Tidy Tuesday")
	+ [Survivor](https://gradientdescending.com/category/survivor/ "Survivor")
	+ [Statistics](https://gradientdescending.com/tag/statistics/ "Statistics")
	+ [Data Science](https://gradientdescending.com/category/data-science/ "Data Science")
* [Survivor](# "Survivor") 
	+ [Posts](https://gradientdescending.com/category/survivor/ "Posts")
	+ [Data](https://docs.google.com/spreadsheets/d/1Xhod9FdVFr69hrX7No40WZAz0ZmhO_5x6WghxawuSno/edit#gid=1849373991 "Data")
		- [R package (Github)](https://github.com/doehm/survivoR "R package (Github)")
		- [Google Sheets](https://docs.google.com/spreadsheets/d/1Xhod9FdVFr69hrX7No40WZAz0ZmhO_5x6WghxawuSno/edit#gid=1849373991 "Google Sheets")
	+ [The Sanctuary](https://gradientdescending.com/the-sanctuary/ "The Sanctuary")
	+ [Confessionals](https://gradientdescending.com/dig-deep/confessional-tables.html "Confessionals")
	+ [Confessional timing app](https://danieloehm.shinyapps.io/survivorDash/ "Confessional timing app")
* [About Me](# "About Me") 
	+ [About Me](https://gradientdescending.com/danieloehm/ "About Me")
	+ [Ultrarunning](https://gradientdescending.com/category/ultrarunning/ "Ultrarunning")
* [Contact](https://gradientdescending.com/contact/ "Contact")
* [Buy me a coffee 🙂☕](https://www.buymeacoffee.com/danoehm "Buy me a coffee 🙂☕")
 














[Data Science](https://gradientdescending.com/category/data-science/) [R](https://gradientdescending.com/category/r/)
Alone R package: Datasets from the survival TV series
=====================================================



January 20, 2023
[Daniel Oehm](https://gradientdescending.com/author/danieloehm/ "Posts by Daniel Oehm")
[0 Comments](https://gradientdescending.com/alone-r-package-datasets-from-the-survival-tv-series/#respond)



I have been watching the survival TV series ‘[Alone](https://www.history.com/shows/alone),’ where 10 survivalists are dropped in an extremely remote area and must fend for themselves. I am super impressed by their skills, endurance, and mental fortitude. To last 100 days in the Arctic winter living off the land is truly impressive.


True to form, I’ve collected the data and I am sharing it here in the {[alone](https://github.com/doehm/alone)} R package.


It is a collection of datasets about the TV series in a tidy format. Included in the package are 4 datasets


* `survivalists`
* `loadouts`
* `episodes`
* `seasons`


For non\-Rstats users here is the link to the [Google sheets doc](https://docs.google.com/spreadsheets/d/1-ZGasLGFVv6t50cOOhcA0SW68jdBIASTh3KFA2o1PQY/edit?usp=sharing).


Installation
------------


Install from CRAN:



```

install.packages("alone")

```

Install from [Github](https://github.com/doehm/alone):



```

devtools::install_github("doehm/alone")

```

Datasets
--------


### survivalists


A data frame of survivalists across all 9 seasons detailing name and demographics, location and profession, result, days lasted, reasons for tapping out (detailed and categorised), and page URL.


Dataset features:


* `season`: The season number
* `name`: Name of the survivalist
* `age`: Age of survivalist
* `gender`: Gender
* `city`: City
* `state`: State
* `country`: Country
* `result`: Place the survivalist finished in the season
* `days_lasted`: The number of days lasted in the game before tapping out or winning
* `medically_evacuated`: Logical. If the survivalist was medically evacuated from the game
* `reason_tapped_out`: The reason the survivalist tapped out of the game. `NA` means they were the winner. Reason being that technically if they won they never tapped out.
* `reason_category`: A simplified category of the reason for tapping out
* `team`: The team they were associated with (only for season 4\)
* `day_linked_up`: Day the team members linked up (only for season 4\)
* `profession`: Profession
* `url`: URL of cast page on the history channel website. Prefix URL with <https://www.history.com/shows/alone/cast>


As an example, use this dataset to compare the number of days survived for both men and women. 



```

library(tidyverse)

df <- expand_grid(
  days_lasted = 0:max(survivalists$days_lasted),
  gender = unique(survivalists$gender)
) |> 
  left_join(
    survivalists |> 
      count(days_lasted, gender),
    by = c("days_lasted", "gender")
  ) |> 
  left_join(
    survivalists |> 
      count(gender, name = "N"),
    by = "gender"
  ) |> 
  group_by(gender) |> 
  mutate(
    n = replace_na(n, 0),
    n_lasted = N-cumsum(n),
    p = n_lasted/N
  ) 

# Kaplan-Meier survival curves
# code is simplified and plot won't match below
df |> 
  ggplot(aes(days_lasted, p, colour = gender)) +
  geom_line() 

# boxplots
survivalists |> 
  ggplot(aes(days_lasted, fill = gender)) +
  geom_boxplot(alpha = 0.5) +
  geom_jitter(width = 0.2, pch = 1, size = 3) +
  theme_minimal()

```

![](opensource/tidytuesday/2023-01-24/images/0.png)
While there is yet to be a female winner, there is some evidence to suggest that women, on average, survive longer than men. Although, we should investigate this further since in the first season there are a lot of early taps and no women, plus the winners should be treated as censored data.


The full code to reproduce the above plot is found [here](https://github.com/doehm/alone/blob/main/dev/scripts/plots.R).


### loadouts


The rules allow each survivalist to take 10 items with them. This dataset includes information on each survivalist’s loadout. It has detailed item descriptions and a simplified version for easier aggregation and analysis.


Dataset features:


* `version`: Country code for the version of the show
* `season`: The season number
* `name`: Name of the survivalist
* `item_number`: Item number
* `item_detailed`: Detailed loadout item description
* `item`: Loadout item. Simplified for aggregation
	+



```

library(forcats)

loadouts |>
  count(item) |>
  mutate(item = fct_reorder(item, n, max)) |>
  ggplot(aes(item, n)) +
  geom_col() +
  geom_text(aes(item, n + 3, label = n), family = ft, size = 12, colour = txt) +
  coord_flip()

```

![](opensource/tidytuesday/2023-01-24/images/1.png)
### episodes


This dataset contains details of each episode including the title, number of viewers, beginning quote, and IMDb rating. New episodes are added at the end of future seasons.


Dataset features:


* `version`: Country code for the version of the show
* `season`: The season number
* `episode_number_overall`: Episode number across seasons
* `episode`: Episode number
* `title`: Episode title
* `air_date`: Date the episode originally aired
* `viewers`: Number of viewers in the US (millions)
* `quote`: The beginning quote
* `author`: Author of the beginning quote
* `imdb_rating`: IMDb rating of the episode
* `n_ratings`: Number of ratings given for the episode


### seasons


The season summary dataset includes location, latitude and longitude, and other season\-level information. It includes the date of drop\-off where the information exists.


Dataset features:


* `version`: Country code for the version of the show
* `season`: The season number
* `location`: Location
* `country`: Country
* `n_survivors`: Number of survivalists in the season. In season 4 there were 7 teams of 2\.
* `lat`: Latitude
* `lon`: Longitude
* `date_drop_off`: The date the survivalists were dropped off


References
----------


If there is any data you would like to include please get in touch.


1. History: <https://www.history.com/shows/alone/cast>
2. Wikipedia: <https://en.wikipedia.org/wiki/Alone_(TV_series)>
3. Wikipedia (episodes): [https://en.wikipedia.org/wiki/List\_of\_Alone\_episodes\#Season\_1\_(2015\)\_\-\_Vancouver\_Island](https://en.wikipedia.org/wiki/List_of_Alone_episodes#Season_1_(2015)_-_Vancouver_Island)


Follow me on social media:* 
* 
* 
* 
* 

 






[alone](https://gradientdescending.com/tag/alone/) [data](https://gradientdescending.com/tag/data/) [dataviz](https://gradientdescending.com/tag/dataviz/) [R](https://gradientdescending.com/tag/r/) [rstats](https://gradientdescending.com/tag/rstats/)





Post navigation
---------------


[Previous Post Select colours from an image in R with {eyedroppeR}](https://gradientdescending.com/select-colours-from-an-image-in-r-with-eyedropper/)[Next Post Do confessionals give away the winner of Survivor?](https://gradientdescending.com/do-confessionals-give-away-the-winner-of-survivor/)










Search for:





![](opensource/tidytuesday/2023-01-24/images/2.png)Bits and PiecesI'm pleased to be a contributor to [**R Bloggers**](https://www.r-bloggers.com/). It is where you will find most of my posts featuring R.The SanctuaryA dedicated space for Survivor stats.

  
  
Quick LinksLinks to Survivor assets:  

- **[The Sanctuary](https://gradientdescending.com/the-sanctuary/index.html)**
- **[survivoR R package Github repo](https://github.com/doehm/survivoR)**
- **[Survivor data (Google Sheets)](https://docs.google.com/spreadsheets/d/1Xhod9FdVFr69hrX7No40WZAz0ZmhO_5x6WghxawuSno/edit#gid=1849373991)**
- **[Birthday Calendar](https://gradientdescending.com/survivor/birthdays/birthdays joined.png)**
  
  

Links to Alone assets:
- **[Alone results table](https://gradientdescending.com/alone/tables/survivalists.html)
- **[Github repo](https://github.com/doehm/alone)
- **[Data (Google Sheets)](https://docs.google.com/spreadsheets/d/1-ZGasLGFVv6t50cOOhcA0SW68jdBIASTh3KFA2o1PQY/edit?usp=sharing)******


Recent Posts
* [📦 {alone} v0\.5 is now available](https://gradientdescending.com/%f0%9f%93%a6-alone-v0-5-is-now-available/)
* [Was Dub right to expect to be done in 60 days?](https://gradientdescending.com/was-dub-right-to-expect-to-be-done-in-60-days/)
* [Wingspan Data Analysis](https://gradientdescending.com/wingspan-data-analysis/)
* [Are the chances of winning Survivor getting better or worse?](https://gradientdescending.com/are-the-chances-of-winning-survivor-getting-better-or-worse/)
* [Who has the best chance of winning Survivor?](https://gradientdescending.com/who-has-the-best-chance-of-winning-survivor/)
* [Can Jury Favorability Predict the Winner of Survivor?](https://gradientdescending.com/can-jury-favorability-predict-the-winner-of-survivor/)
* [Ignoring the IID assumption isn’t a great idea](https://gradientdescending.com/ignoring-the-iid-assumption-isnt-a-great-idea/)
* [{alone} v0\.4 is now available](https://gradientdescending.com/alone-v0-4-is-now-available/)
* [The Sanctuary: Stats and data from {survivoR}](https://gradientdescending.com/the-sanctuary-stats-and-data-from-survivor/)
* [{survivoR} 2\.3\.3 is now available](https://gradientdescending.com/survivor-2-3-3-is-now-available/)


Archives Archives

Select Month
 September 2024  (2\)
 August 2024  (1\)
 July 2024  (2\)
 June 2024  (4\)
 May 2024  (1\)
 April 2024  (1\)
 March 2024  (1\)
 January 2024  (3\)
 December 2023  (3\)
 November 2023  (5\)
 October 2023  (5\)
 September 2023  (3\)
 June 2023  (3\)
 May 2023  (2\)
 April 2023  (1\)
 January 2023  (1\)
 December 2022  (1\)
 September 2022  (1\)
 July 2022  (1\)
 June 2022  (2\)
 May 2022  (3\)
 March 2022  (1\)
 April 2021  (1\)
 January 2021  (1\)
 August 2020  (1\)
 June 2020  (1\)
 April 2020  (1\)
 October 2019  (1\)
 September 2019  (1\)
 August 2019  (1\)
 May 2019  (2\)
 April 2019  (3\)
 March 2019  (1\)
 February 2019  (2\)
 January 2019  (1\)
 December 2018  (1\)
 November 2018  (2\)
 October 2018  (1\)
 September 2018  (2\)
 August 2018  (1\)
 July 2018  (4\)
 June 2018  (5\)
 May 2018  (6\)


Categories
* [Data Science](https://gradientdescending.com/category/data-science/) 54
* [Python](https://gradientdescending.com/category/python/) 2
* [R](https://gradientdescending.com/category/r/) 51
* [Survivor](https://gradientdescending.com/category/survivor/) 17
* [Tidy Tuesday](https://gradientdescending.com/category/tidy-tuesday/) 16
* [Ultrarunning](https://gradientdescending.com/category/ultrarunning/) 2


Meta
* [Log in](https://gradientdescending.com/wp-login.php)
* [Entries feed](https://gradientdescending.com/feed/)
* [Comments feed](https://gradientdescending.com/comments/feed/)
* [WordPress.org](https://wordpress.org/)


 










Categories
* [Data Science](https://gradientdescending.com/category/data-science/) 54
* [Python](https://gradientdescending.com/category/python/) 2
* [R](https://gradientdescending.com/category/r/) 51
* [Survivor](https://gradientdescending.com/category/survivor/) 17
* [Tidy Tuesday](https://gradientdescending.com/category/tidy-tuesday/) 16
* [Ultrarunning](https://gradientdescending.com/category/ultrarunning/) 2


 


 


Meta
* [Log in](https://gradientdescending.com/wp-login.php)
* [Entries feed](https://gradientdescending.com/feed/)
* [Comments feed](https://gradientdescending.com/comments/feed/)
* [WordPress.org](https://wordpress.org/)


 






 © 2024 Dan Oehm \| Gradient Descending. All rights reserved. 

 Theme by [WPWarfare](https://wpwarfare.com/) Powered by [WordPress](http://wordpress.org/) 




























survivoR \| Data from the TV series in R \- Dan Oehm \| Gradient Descending







































































Toggle navigation




[Dan Oehm \| Gradient Descending](http://gradientdescending.com/)
=================================================================

 
* [Blog](# "Blog") 
	+ [All](http://gradientdescending.com "All")
	+ [R](http://gradientdescending.com/category/r/ "R")
	+ [Tidy Tuesday](http://gradientdescending.com/category/tidy-tuesday/ "Tidy Tuesday")
	+ [Survivor](http://gradientdescending.com/category/survivor/ "Survivor")
	+ [Statistics](http://gradientdescending.com/tag/statistics/ "Statistics")
	+ [Data Science](http://gradientdescending.com/category/data-science/ "Data Science")
* [Survivor](# "Survivor") 
	+ [Posts](http://gradientdescending.com/category/survivor/ "Posts")
	+ [Data](https://docs.google.com/spreadsheets/d/1Xhod9FdVFr69hrX7No40WZAz0ZmhO_5x6WghxawuSno/edit#gid=1849373991 "Data")
		- [R package (Github)](https://github.com/doehm/survivoR "R package (Github)")
		- [Google Sheets](https://docs.google.com/spreadsheets/d/1Xhod9FdVFr69hrX7No40WZAz0ZmhO_5x6WghxawuSno/edit#gid=1849373991 "Google Sheets")
	+ [The Sanctuary](https://gradientdescending.com/the-sanctuary/ "The Sanctuary")
	+ [Confessionals](https://gradientdescending.com/dig-deep/confessional-tables.html "Confessionals")
	+ [Confessional timing app](https://danieloehm.shinyapps.io/survivorDash/ "Confessional timing app")
* [About Me](# "About Me") 
	+ [About Me](http://gradientdescending.com/danieloehm/ "About Me")
	+ [Ultrarunning](http://gradientdescending.com/category/ultrarunning/ "Ultrarunning")
* [Contact](http://gradientdescending.com/contact/ "Contact")
* [Buy me a coffee 🙂☕](https://www.buymeacoffee.com/danoehm "Buy me a coffee 🙂☕")
 














[R](http://gradientdescending.com/category/r/)
survivoR \| Data from the TV series in R
========================================



January 18, 2021
[Daniel Oehm](http://gradientdescending.com/author/danieloehm/ "Posts by Daniel Oehm")
[0 Comments](http://gradientdescending.com/survivor-data-from-the-tv-series-in-r/#respond)



596 episodes. 40 seasons. 1 package!


I’m a pretty big fan of Survivor and have religiously watched every season since the first. With 40 seasons under its belt, there’s a tonne of data to dive into. However, getting that data in one place has been tedious. Hence, the survivoR package.


survivoR is a collection of datasets detailing events across all 40 seasons of the US Survivor, including castaway information, vote history, immunity and reward challenge winners, jury votes, and viewers.


Installation
------------


survivoR is now on CRAN. Install the package using



```

install.packages("survivoR")

```

Or from [Github](https://github.com/doehm/survivoR) with the following.



```

devtools::install_github("doehm/survivoR")

```

Dataset overview
----------------


Below are all the datasets that are contained within the package.


### Season summary


A data frame containing summary details of each season of Survivor, including the winner, runner ups and location. This is a nested data frame given there maybe 1 or 2 runner\-ups. By using a nested data frame the grain is maintained to 1 row per season.



```

season_summary

```


```

#> # A tibble: 40 x 17
#>    season_name season location country tribe_setup full_name winner runner_ups
#>    <chr>        <int> <chr>    <chr>   <chr>       <glue> <chr>    <list>    
#>  1 Survivor: ~      1 Pulau T~ Malays~ Two tribes~ Richa~ Richard  <tibble [~
#>  2 Survivor: ~      2 Herbert~ Austra~ Two tribes~ Tina ~ Tina     <tibble [~
#>  3 Survivor: ~      3 Shaba N~ Kenya   Two tribes~ Ethan~ Ethan    <tibble [~
#>  4 Survivor: ~      4 Nuku Hi~ Polyne~ Two tribes~ Vecep~ Vecepia  <tibble [~
#>  5 Survivor: ~      5 Ko Taru~ Thaila~ Two tribes~ Brian~ Brian    <tibble [~
#>  6 Survivor: ~      6 Rio Neg~ Brazil  Two tribes~ Jenna~ Jenna    <tibble [~
#>  7 Survivor: ~      7 Pearl I~ Panama  Two tribes~ Sandr~ Sandra   <tibble [~
#>  8 Survivor: ~      8 Pearl I~ Panama  Three trib~ Amber~ Amber    <tibble [~
#>  9 Survivor: ~      9 Efate, ~ Vanuatu Two tribes~ Chris~ Chris    <tibble [~
#> 10 Survivor: ~     10 Koror, ~ Palau   A schoolya~ Tom W~ Tom      <tibble [~
#> # ... with 30 more rows, and 9 more variables: final_vote <chr>,
#> #   timeslot <chr>, premiered <date>, premier_viewers <dbl>, ended <date>,
#> #   finale_viewers <dbl>, reunion_viewers <dbl>, rank <dbl>, viewers <dbl>

```


```

season_summary %>%
  select(season, viewers_premier, viewers_finale, viewers_reunion, viewers_mean) %>%
  pivot_longer(cols = -season, names_to = "episode", values_to = "viewers") %>%
  mutate(
    episode = to_title_case(str_replace(episode, "viewers_", ""))
  ) %>%
  ggplot(aes(x = season, y = viewers, colour = episode)) +
  geom_line() +
  geom_point(size = 2) +
  theme_minimal() +
  scale_colour_survivor(16) +
  labs(
    title = "Survivor viewers over the 40 seasons",
    x = "Season",
    y = "Viewers (Millions)",
    colour = "Episode"
  )

```

![](opensource/tidytuesday/2021-06-01/images/0.png)

The number of viewers for each season of Survivor has been steadily decreasing, however the mean number of viewers has only dropped by 3\-4 million over the last 20 seasons (or 10 years). 


### Castaways


Season and demographic information about each castaway. Within a season the data is ordered by the first voted out to sole survivor indicated by `order` which represents the order they castaways left the island. This may be by being voted off the island, being evacuated due to medical reasons, or quitting. When demographic information is missing, it likely means that the castaway re\-entered the game at a later stage by winning the opportunity to return. Castaways that have played in multiple seasons will feature more than once with the age and location representing that point in time.



```

castaways %>% 
  filter(season == 40)

```


```

#> # A tibble: 22 x 15
#>    season_name season castaway nickname age   city  state   day original_tribe
#>    <chr>        <dbl> <chr>    <chr>    <chr> <chr> <chr> <dbl> <chr>         
#>  1 Survivor: ~     40 Natalie~ Natalie  <NA>  <NA>  <NA>      2 Sele          
#>  2 Survivor: ~     40 Amber M~ Amber    40    Pens~ Flor~     3 Dakal         
#>  3 Survivor: ~     40 Danni B~ Danni    43    Shaw~ Kans~     6 Sele          
#>  4 Survivor: ~     40 Ethan Z~ Ethan    45    Hill~ New ~     9 Sele          
#>  5 Survivor: ~     40 Tyson A~ Tyson    <NA>  <NA>  <NA>     11 Dakal         
#>  6 Survivor: ~     40 Rob Mar~ Rob      43    Pens~ Flor~    14 Sele          
#>  7 Survivor: ~     40 Parvati~ Parvati  36    Los ~ Cali~    16 Sele          
#>  8 Survivor: ~     40 Sandra ~ Sandra   44    Rive~ Flor~    16 Dakal         
#>  9 Survivor: ~     40 Yul Kwon Yul      44    Los ~ Cali~    18 Dakal         
#> 10 Survivor: ~     40 Wendell~ Wendell  35    Phil~ Penn~    21 Dakal         
#> # ... with 12 more rows, and 6 more variables: merged_tribe <chr>,
#> #   result <chr>, jury_status <chr>, order <int>, swapped_tribe <chr>,
#> #   swapped_tribe2 <chr>

```

### Vote history


This data frame contains a complete history of votes cast across all seasons of Survivor. This allows you to see who voted for who at which tribal council. It also includes details on who had individual immunity as well as who had their votes nullified by a hidden immunity idol. This details the key events for the season. 


While there are consistent events across the seasons such as the tribe swap, there are some unique events such as the ‘mutiny’ in Survivor: Cook Islands (Season 13\) or the ‘Outcasts’ in Survivor: Pearl Islands (season 7\). When castaways change tribes by some means other than a tribe swap, it is still recorded as ‘swapped’ to maintain a standard. 


The data is recorded as ‘swapped’ with a trailing digit if a swap has occurred more than once. This includes absorbed tribes when 3 tribes are reduced to 2 or when Stephanie was ‘absorbed’ in Survivor: Palau (season 10\) when everyone but herself was voted off the tribe (and making Palau one of the classic seasons of Survivor). To indicate a change in tribe status these events are also considered ‘swapped’.


This data frame is at the tribal council by castaway grain, so there is a vote for everyone that attended the tribal council. However, there are some edge cases such as when the ‘steal a vote’ advantage is played. In this case, there is a second row for the castaway indicating their second vote.


In the case of a tie and a revote, the first vote is recorded and the result is recorded as ‘Tie’. The deciding vote is recorded as normal. Where there is a double tie, it is recorded as ‘Tie2’ (for lack of a better name). In the case of a double tie and it goes to rocks, the vote is either ‘Black rock’ or ‘White rock’. In the older episodes of Survivor, when there were two ties in a row, rather than going to rocks there was a countback of votes. 



```

vh <- vote_history %>% 
  filter(
    season == 40,
    episode == 10
  )
vh

```


```

#> # A tibble: 9 x 11
#>   season_name season episode   day tribe_status castaway immunity vote 
#>   <chr>        <dbl>   <dbl> <dbl> <chr>        <chr>    <chr>    <chr>
#> 1 Survivor: ~     40      10    25 merged       Tony     individ~ Tyson
#> 2 Survivor: ~     40      10    25 merged       Michele  <NA>     Tyson
#> 3 Survivor: ~     40      10    25 merged       Sarah    <NA>     Deni~
#> 4 Survivor: ~     40      10    25 merged       Sarah    <NA>     Tyson
#> 5 Survivor: ~     40      10    25 merged       Ben      <NA>     Tyson
#> 6 Survivor: ~     40      10    25 merged       Nick     <NA>     Tyson
#> 7 Survivor: ~     40      10    25 merged       Kim      <NA>     Soph~
#> 8 Survivor: ~     40      10    25 merged       Sophie   <NA>     Deni~
#> 9 Survivor: ~     40      10    25 merged       Tyson    <NA>     Soph~
#> # ... with 3 more variables: nullified <lgl>, voted_out <chr>, order <dbl>

```


```

vh %>% 
  count(vote)

```


```

#> # A tibble: 5 x 2
#>   vote       n
#>   <chr>  <int>
#> 1 Denise     2
#> 2 Immune     1
#> 3 None       1
#> 4 Sophie     2
#> 5 Tyson      5

```

Events in the game such as fire challenges, rock draws, steal\-a\-vote advantages, or countbacks (in the early days) often mean a vote wasn’t placed for an individual. Rather a challenge may be won, lost, no vote cast, etc but attended tribal council. These events are recorded in the `vote` field. I have included a function `clean_votes` for when only the votes cast for individuals are needed. If the input data frame has the `vote` column it can simply be piped.



```

vh %>% 
  clean_votes() %>%
  count(vote)

```


```

#> # A tibble: 3 x 2
#>   vote       n
#>   <chr>  <int>
#> 1 Denise     2
#> 2 Sophie     2
#> 3 Tyson      5

```

### Challenges


A nested tidy data frame of immunity and reward challenge results. The winners and winning tribe of the challenge are found by expanding the `winners` column. For individual immunity challenges the winning tribe is simply `NA`.



```

challenges %>% 
  filter(season == 40)

```


```

#> # A tibble: 28 x 7
#>    season_name      season episode title          day challenge_type winners    
#>    <chr>             <dbl>   <dbl> <chr>        <dbl> <chr>          <list>     
#>  1 Survivor: Winne~     40       1 Greatest of~     2 reward         <tibble[,2~
#>  2 Survivor: Winne~     40       1 Greatest of~     2 immunity       <tibble[,2~
#>  3 Survivor: Winne~     40       1 Greatest of~     3 immunity       <tibble[,2~
#>  4 Survivor: Winne~     40       2 It's Like a~     6 reward         <tibble[,2~
#>  5 Survivor: Winne~     40       2 It's Like a~     6 immunity       <tibble[,2~
#>  6 Survivor: Winne~     40       3 Out for Blo~     9 reward         <tibble[,2~
#>  7 Survivor: Winne~     40       3 Out for Blo~     9 immunity       <tibble[,2~
#>  8 Survivor: Winne~     40       4 I Like Reve~    11 reward         <tibble[,2~
#>  9 Survivor: Winne~     40       4 I Like Reve~    11 immunity       <tibble[,2~
#> 10 Survivor: Winne~     40       5 The Buddy S~    14 immunity       <tibble[,2~
#> # ... with 18 more rows

```

Typically in the merge, if a single person wins a reward they are allowed to bring others along with them. The first castaway in the expanded list is likely to be the winner and the subsequent players those they brought along with them. Although, not always. Occasionally in the merge, the castaways are split into two teams for the purpose of the reward, in which case all castaways win the reward rather than a single person.


The `day` field on this data set represents the day of the tribal council rather than the day of the challenge. This is to more easily associate the reward challenge with the immunity challenge and result of the tribal council. It also helps for joining tables.


Note the challenges table is the combined immunity and rewards tables which will eventually be dropped in later releases.


### Jury votes


This data frame contains the history of jury votes. It is more verbose than it needs to be. However, having a 0\-1 column indicating if a vote was placed for the finalist makes it easier to summarise castaways that received no votes.



```

jury_votes %>% 
  filter(season == 40)

```


```

#> # A tibble: 48 x 5
#>    season_name              season castaway finalist  vote
#>    <chr>                     <dbl> <chr>    <chr>    <dbl>
#>  1 Survivor: Winners at War     40 Sarah    Michele      0
#>  2 Survivor: Winners at War     40 Sarah    Natalie      0
#>  3 Survivor: Winners at War     40 Sarah    Tony         1
#>  4 Survivor: Winners at War     40 Ben      Michele      0
#>  5 Survivor: Winners at War     40 Ben      Natalie      0
#>  6 Survivor: Winners at War     40 Ben      Tony         1
#>  7 Survivor: Winners at War     40 Denise   Michele      0
#>  8 Survivor: Winners at War     40 Denise   Natalie      0
#>  9 Survivor: Winners at War     40 Denise   Tony         1
#> 10 Survivor: Winners at War     40 Nick     Michele      0
#> # ... with 38 more rows

```


```

jury_votes %>% 
  filter(season == 40) %>% 
  group_by(finalist) %>% 
  summarise(votes = sum(vote))


```


```

#> # A tibble: 3 x 2
#>   finalist votes
#>   <chr>    <dbl>
#> 1 Michele      0
#> 2 Natalie      4
#> 3 Tony        12

```

### Viewers


A data frame containing the viewer information for every episode across all seasons. It also includes the rating and viewer share information for viewers aged 18 to 49 years.



```

viewers %>% 
  filter(season == 40)

```


```

#> # A tibble: 14 x 9
#>    season_name season episode_number_~ episode title episode_date viewers
#>    <chr>        <dbl>            <dbl>   <dbl> <chr> <date>         <dbl>
#>  1 Survivor: ~     40              583       1 Grea~ 2020-02-12      6.68
#>  2 Survivor: ~     40              584       2 It's~ 2020-02-19      7.16
#>  3 Survivor: ~     40              585       3 Out ~ 2020-02-26      7.14
#>  4 Survivor: ~     40              586       4 I Li~ 2020-03-04      7.08
#>  5 Survivor: ~     40              587       5 The ~ 2020-03-11      6.91
#>  6 Survivor: ~     40              588       6 Quic~ 2020-03-18      7.83
#>  7 Survivor: ~     40              589       7 We'r~ 2020-03-25      8.18
#>  8 Survivor: ~     40              590       8 This~ 2020-04-01      8.23
#>  9 Survivor: ~     40              591       9 War ~ 2020-04-08      7.85
#> 10 Survivor: ~     40              592      10 The ~ 2020-04-15      8.14
#> 11 Survivor: ~     40              593      11 This~ 2020-04-22      8.16
#> 12 Survivor: ~     40              594      12 Frie~ 2020-04-29      8.08
#> 13 Survivor: ~     40              595      13 The ~ 2020-05-06      7.57
#> 14 Survivor: ~     40              596      14 It A~ 2020-05-13      7.94
#> # ... with 2 more variables: rating_18_49 <dbl>, share_18_49 <dbl>

```

### Tribe colours


This data frame contains the tribe names and colours for each season, including the RGB values. These colours can be joined with the other data frames to customise colours for plots. Another option is to add tribal colours to ggplots with the scale functions. 



```

tribe_colours

#> # A tibble: 139 x 7
#>    season_name                  season tribe_name     r     g     b tribe_colour
#>    <chr>                         <dbl> <chr>      <dbl> <dbl> <dbl> <chr>       
#>  1 Survivor: Winners at War         40 Sele           0   103   214 #0067D6     
#>  2 Survivor: Winners at War         40 Dakal        216    14    14 #D80E0E     
#>  3 Survivor: Winners at War         40 Yara           4   148    81 #049451     
#>  4 Survivor: Winners at War         40 Koru           0     0     0 #000000     
#>  5 Survivor: Island of the Ido~     39 Lairo        243   148    66 #F39442     
#>  6 Survivor: Island of the Ido~     39 Vokai        217   156   211 #D99CD3     
#>  7 Survivor: Island of the Ido~     39 Lumuwaku      48    78   210 #304ED2     
#>  8 Survivor: Edge of Extinction     38 Manu          16    80   186 #1050BA     
#>  9 Survivor: Edge of Extinction     38 Lesu           0   148   128 #009480     
#> 10 Survivor: Edge of Extinction     38 Kama         250   207    34 #FACF22     
#> # ... with 129 more rows

```



Tribe colours for each season of Survivor


ggplot2 scale functions
-----------------------


Included are ggplot2 scale functions of the form `scale_fill_survivor()` and `scale_fill_tribes()` to add season and tribe colours to ggplot. The `scale_fill_survivor()` scales uses a colour palette extracted from the season logo and `scale_fill_tribes()` scales uses the tribal colours of the specified season as a colour palette.


Simply input the desired season number. If no season is provided it will default to season 40\.




```

castaways %>% 
  count(season, personality_type) %>% 
  ggplot(aes(x = season, y = n, fill = personality_type)) +
  geom_bar(stat = "identity") +
  scale_fill_survivor(40) +
  theme_minimal()

```

![](opensource/tidytuesday/2021-06-01/images/1.png)
Below are the palettes for all seasons.




To use the tribe scales, simply input the season number desired to use those tribe colours. If the fill or colour aesthetic is the tribe name, this needs to be passed to the scale function as `scale_fill_tribes(season, tribe = tribe)` (for now) where `tribe` is on the input data frame. If the fill or colour aesthetic is independent from the actual tribe names, like gender for example, `tribe` does not need to be specified and will simply use the tribe colours as a colour palette, such as the viewers line graph above.



```

ssn <- 35
labels <- castaways %>%
  filter(
    season == ssn,
    str_detect(result, "Sole|unner")
  ) %>%
  mutate(label = glue("{castaway} ({original_tribe})")) %>%
  select(label, castaway)

jury_votes %>%
  filter(season == ssn) %>%
  left_join(
    castaways %>%
      filter(season == ssn) %>%
      select(castaway, original_tribe),
    by = "castaway"
  ) %>%
  group_by(finalist, original_tribe) %>%
  summarise(votes = sum(vote)) %>%
  left_join(labels, by = c("finalist" = "castaway")) %>%
  {
    ggplot(., aes(x = label, y = votes, fill = original_tribe)) +
      geom_bar(stat = "identity", width = 0.5) +
      scale_fill_tribes(ssn, tribe = .$original_tribe) +
      theme_minimal() +
      labs(
        x = "Finalist (original tribe)",
        y = "Votes",
        fill = "Original\ntribe",
        title = "Votes received by each finalist"
      )
  }

```

![](opensource/tidytuesday/2021-06-01/images/2.png)
Visualise the events of each season
-----------------------------------


This data provides a way to deeper analyse each season and the plays within each episode. For example, we could construct a graph of who voted for who, where the castaway is the node and the edge is who they voted for using the vote history data. While in this representation it’s possible to use clustering algorithms to identify alliances in the data. Other uses include identifying the probability of players jumping ship and pivotal votes. This is particularly interesting for the first 1 or 2 tribals of the merge to see if players stick with their original tribe or jump ship.



```

library(extrafont)
loadfonts()

ft <- "Segoe UI Light"

ssn <- 40

df <- vote_history %>%
  filter(
    season == ssn,
    order == 13
  )

nodes <- df %>%
  distinct(castaway) %>%
  mutate(id = 1:n()) %>%
  rename(label = castaway)

edges <- df %>%
  count(castaway, vote) %>%
  left_join(
    nodes %>%
      rename(from = id),
    by = c("castaway" = "label")
  ) %>%
  left_join(
    nodes %>%
      rename(to = id),
    by = c("vote" = "label")
  ) %>%
  mutate(arrows = "to") %>%
  rename(value = n) %>%
  left_join(
    castaways %>%
      filter(season == ssn) %>%
      select(castaway, original_tribe),
    by = "castaway"
  )

labels <- edges %>%
  select(from, to, castaway, original_tribe) %>%
  distinct(from, castaway, original_tribe) %>%
  arrange(castaway) %>%
  left_join(
    edges %>%
      count(vote),
    by = c("castaway" = "vote")
  )

cols <- tribe_colours$tribe_colour
names(cols) <- tribe_colours$tribe
ggraph(
  edges %>% 
    rename(`Original tribe` = original_tribe), 
  layout = "linear") +
  geom_edge_arc(aes(colour = `Original tribe`), arrow = arrow(length = unit(4, "mm"), type = "closed"), end_cap = circle(10, 'mm')) +
  geom_node_point(size = 26, colour = cols[labels$original_tribe]) +
  geom_node_point(size = 24, colour = "black") +
  geom_node_text(aes(label = labels$castaway), colour = "grey", size = 4, vjust = 0, family = ft) +
  geom_node_text(aes(label = labels$n), colour = "grey", size = 4, vjust = 2, family = ft) +
  scale_edge_colour_manual(values = cols[unique(edges$original_tribe)]) +
  scale_colour_manual(values = cols[unique(edges$original_tribe)]) +
  theme_graph()

```

[![](opensource/tidytuesday/2021-06-01/images/3.png)](http://gradientdescending.com/?attachment_id=1644)

Vote distribution for episode 11 of Survivor: Winners at War. Sophie was the 13th person voted off the island


New features and future seasons
-------------------------------


I intend to update the survivoR package each week during the airing of future seasons. For Survivor and data nuts like myself, this will enable a deeper analysis of each episode, and just neat ways visualise the evolution of the game.


New features will be added, such as details on exiled castaways across the seasons. If you have a request for specific data let me know in the comments and I’ll see what I can do. Also, if you’d like to contribute by adding to existing datasets or contribute a new dataset, please contact me directly on the [contacts](http://gradientdescending.com/contact/) page.


Issues
------


Given the variable nature of the game of Survivor and how the rules are tweaked each season, there are bound to be edge cases where the data is not quite right. Please log an issue on [Github](https://github.com/doehm/survivoR), or with me directly in the comments and I will correct the datasets.


References
----------


Data in the survivoR package was mostly sourced from [Wikipedia](https://en.wikipedia.org/wiki/Survivor_(American_TV_series)). Other data, such as the tribe colours, was manually recorded and entered myself.


Torch graphic in hex: [Fire Torch Vectors by Vecteezy](https://www.vecteezy.com/free-vector/fire-torch)


Appendix
--------


If R isn’t your thing you can download an XLSX of the data R data files [here](http://gradientdescending.com/data/survivoR.xlsx)


Follow me on social media:* 
* 
* 
* 
* 

 






[data](http://gradientdescending.com/tag/data/) [r package](http://gradientdescending.com/tag/r-package/) [rstats](http://gradientdescending.com/tag/rstats/) [survivor](http://gradientdescending.com/tag/survivor/)





Post navigation
---------------


[Previous Post Don’t get fooled by the Gambler’s Fallacy](http://gradientdescending.com/dont-get-fooled-by-the-gamblers-fallacy/)[Next Post survivoR now on CRAN!](http://gradientdescending.com/survivor-now-on-cran/)










Search for:





Bits and PiecesI'm pleased to be a contributor to [**R Bloggers**](https://www.r-bloggers.com/). It is where you will find most of my posts featuring R.The SanctuaryA dedicated space for Survivor stats.

  
  
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
* [📦 {alone} v0\.5 is now available](http://gradientdescending.com/%f0%9f%93%a6-alone-v0-5-is-now-available/)
* [Was Dub right to expect to be done in 60 days?](http://gradientdescending.com/was-dub-right-to-expect-to-be-done-in-60-days/)
* [Wingspan Data Analysis](http://gradientdescending.com/wingspan-data-analysis/)
* [Are the chances of winning Survivor getting better or worse?](http://gradientdescending.com/are-the-chances-of-winning-survivor-getting-better-or-worse/)
* [Who has the best chance of winning Survivor?](http://gradientdescending.com/who-has-the-best-chance-of-winning-survivor/)
* [Can Jury Favorability Predict the Winner of Survivor?](http://gradientdescending.com/can-jury-favorability-predict-the-winner-of-survivor/)
* [Ignoring the IID assumption isn’t a great idea](http://gradientdescending.com/ignoring-the-iid-assumption-isnt-a-great-idea/)
* [{alone} v0\.4 is now available](http://gradientdescending.com/alone-v0-4-is-now-available/)
* [The Sanctuary: Stats and data from {survivoR}](http://gradientdescending.com/the-sanctuary-stats-and-data-from-survivor/)
* [{survivoR} 2\.3\.3 is now available](http://gradientdescending.com/survivor-2-3-3-is-now-available/)


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
* [Data Science](http://gradientdescending.com/category/data-science/) 54
* [Python](http://gradientdescending.com/category/python/) 2
* [R](http://gradientdescending.com/category/r/) 51
* [Survivor](http://gradientdescending.com/category/survivor/) 17
* [Tidy Tuesday](http://gradientdescending.com/category/tidy-tuesday/) 16
* [Ultrarunning](http://gradientdescending.com/category/ultrarunning/) 2


Meta
* [Log in](http://gradientdescending.com/wp-login.php)
* [Entries feed](http://gradientdescending.com/feed/)
* [Comments feed](http://gradientdescending.com/comments/feed/)
* [WordPress.org](https://wordpress.org/)


 










Categories
* [Data Science](http://gradientdescending.com/category/data-science/) 54
* [Python](http://gradientdescending.com/category/python/) 2
* [R](http://gradientdescending.com/category/r/) 51
* [Survivor](http://gradientdescending.com/category/survivor/) 17
* [Tidy Tuesday](http://gradientdescending.com/category/tidy-tuesday/) 16
* [Ultrarunning](http://gradientdescending.com/category/ultrarunning/) 2


 


 


Meta
* [Log in](http://gradientdescending.com/wp-login.php)
* [Entries feed](http://gradientdescending.com/feed/)
* [Comments feed](http://gradientdescending.com/comments/feed/)
* [WordPress.org](https://wordpress.org/)


 






 © 2024 Dan Oehm \| Gradient Descending. All rights reserved. 

 Theme by [WPWarfare](https://wpwarfare.com/) Powered by [WordPress](http://wordpress.org/) 




















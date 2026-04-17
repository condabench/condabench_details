





Analyzing Himalayan peaks and first ascents · Alex Cookson
























[Alex Cookson](https://alexcookson.com/)

* [Home](https://alexcookson.com/)
* [Posts](https://alexcookson.com/post/)
* [About](https://alexcookson.com/about/)




* [Twitter](https://twitter.com/alexcookson)
* [LinkedIn](https://linkedin.com/in/alexcookson)
* [GitHub](https://github.com/tacookson)





© 2020\. All rights reserved.


Built with [Hugo](https://gohugo.io/)
Theme [Blackburn](https://github.com/yoshiharuyamashita/blackburn)





Analyzing Himalayan peaks and first ascents
===========================================








Mar 22, 2020



[data exploration](https://alexcookson.com/tags/data-exploration) /
 
 [bar graphs](https://alexcookson.com/tags/bar-graphs) /
 
 [annotations](https://alexcookson.com/tags/annotations)


 


In this series of posts, we will analyze climbing expeditions to the Himalayas, a mountain range comprising over 50 mountains, including [Mount Everest](https://en.wikipedia.org/wiki/Mount_Everest), the tallest mountain in the world.  

 


This is *Part 1* of a two\-part series:


* Part 1 (this post) looks at Himalayan peaks and their first ascents
* [Part 2 looks at how dangerous it is to climb Everest](https://www.alexcookson.com/post/how-dangerous-is-climbing-mount-everest/)


This post will focus on getting an overview of the Himalayan peaks, especially their height, whether they’ve been summitted, and (if it applies) when the first ascent was and who was involved.  

 



The Himalayan Database
----------------------


The data comes from [The Himalayan Database](https://www.himalayandatabase.com/), a truly impressive and comprehensive dataset with records on over 10,000 climbing expeditions from 1905 to 2019 for more than 450 significant peaks in the Nepal Himalayas. According to the database website:



> The Himalayan Database is a compilation of records for all expeditions that have climbed in the Nepal Himalaya. The database is based on the expedition archives of Elizabeth Hawley, a longtime journalist based in Kathmandu, and it is supplemented by information gathered from books, alpine journals and correspondence with Himalayan climbers.


You can download a program from the website to explore the database, but it uses Microsoft Visual FoxPro, an older program that Miscrosoft no longer supports. I couldn’t get it working, but I was able to read the database tables directly and convert them into CSV files.  

 




Setup
-----


First, we’ll load the `tidyverse` and some other useful packages:


* `fishualize` for ggplot2 colour palettes [inspired by fish](https://cran.r-project.org/web/packages/fishualize/vignettes/overview_colors.html). A big thank you to [Nina Schiettekatte](https://twitter.com/NinaSchiett/status/1180070737471852545) for making this package and [Maia Pelletier](https://twitter.com/MaiaPelletier/status/1242869023437664259) for introducing it to me!
* `scales` for turning ugly numbers into pretty numbers (e.g., 0\.3 to 30%)
* `extrafont` for additional fonts to use in graphs (I like [Bahnschrift / DIN 1451](https://en.wikipedia.org/wiki/DIN_1451))


We’ll also set a default `ggplot2` theme and import our data. `peaks` has information on the peaks themselves, `expeditions` details individual expeditions, and `members` looks at individual members of those expeditions.



```
library(tidyverse)
library(fishualize)
library(scales)
library(extrafont)

theme_set(theme_light())

peaks <- readr::read_csv("https://raw.githubusercontent.com/tacookson/data/master/himalayan-expeditions/peaks.csv")
expeditions <- readr::read_csv("https://raw.githubusercontent.com/tacookson/data/master/himalayan-expeditions/expeditions.csv")
members <- readr::read_csv("https://raw.githubusercontent.com/tacookson/data/master/himalayan-expeditions/members.csv")
```

 




Data inspection
---------------


Even though we’re loading all the tables, our focus is on getting a general sense of the peaks, so we will almost exclusively use the `peaks` dataset. Let’s take a look.



```
peaks %>%
  glimpse()
```


```
## Rows: 468
## Columns: 8
## $ peak_id                    <chr> "AMAD", "AMPG", "ANN1", "ANN2", "ANN3", ...
## $ peak_name                  <chr> "Ama Dablam", "Amphu Gyabjen", "Annapurn...
## $ peak_alternative_name      <chr> "Amai Dablang", NA, NA, NA, NA, NA, NA, ...
## $ height_metres              <dbl> 6814, 5630, 8091, 7937, 7555, 7525, 8026...
## $ climbing_status            <chr> "Climbed", "Climbed", "Climbed", "Climbe...
## $ first_ascent_year          <dbl> 1961, 1953, 1950, 1960, 1961, 1955, 1974...
## $ first_ascent_country       <chr> "New Zealand, USA, UK", "UK", "France", ...
## $ first_ascent_expedition_id <chr> "AMAD61101", "AMPG53101", "ANN150101", "...
```

We have the name and height of the peaks (including any alternative names), whether they’ve been summitted, and the year and countries associated with the first ascent for peaks that *have* been summitted. Countries are listed if an expedition member who reached the summit was a citizen of that country. It’s possible for countries to have citizens in an expedition, but not listed here are part of the first ascent. For example, the first ascent of Mount Everest lists two countries – India (for Tenzing Norgay) and New Zealand (for Edmund Hillary) – even though non\-summitting expedition members included people from the United Kingdom and Nepal.


(Note: there is some [debate about Tenzing Norgay’s nationality](https://en.wikipedia.org/wiki/Talk%3ATenzing_Norgay#Tenzing_Norgay's_nationality). I’m not even close to an expert on this topic, so I will defer to the records in the Himalayan Database, which lists his citizenship as “India”.)  

 




How tall are Himalayan peaks?
-----------------------------


People generally know that Mount Everest is the tallest mountain in the world, but I personally don’t know much about other Himalayan peaks. How tall are they?


We’re going to use the “Pseudocheilinus\_tetrataenia” palette from the `fishualize` package. I can’t get over how much I *love* the colours in this package. [Here](https://www.fishkeeper.co.uk/help-and-advice/marine/wrasses/four-lined-wrasse) is a picture of the fish that inspired the palette we’re using.



```
peaks %>%
  ggplot(aes(height_metres)) +
  geom_histogram(
    binwidth = 200,
    fill = fish(1, option = "Pseudocheilinus_tetrataenia", direction = -1),
    alpha = 0.8
  ) +
  annotate("text", 8450, 17, label = "Mount Everest", family = "Bahnschrift") +
  annotate(
    "curve",
    x = 8500,
    y = 15,
    xend = 8775,
    yend = 2,
    curvature = -0.25,
    arrow = arrow(length = unit(2, "mm"))
  ) +
  labs(
    title = "How tall are Himalayan peaks?",
    caption = "Source: The Himalayan Database",
    x = "Height (m)",
    y = "Number of peaks"
  ) +
  theme(text = element_text(family = "Bahnschrift"))
```

![](opensource/tidytuesday/2020-09-22/images/0.png)


Not surprisingly, Mount Everest is the tallest at almost 9,000 metres. There is a small group of other very tall mountains that are part of a group referred to as [8000ers](https://www.mountainiq.com/guides/eight-thousanders/), something I learned while researching for this post. Most peaks are between 6,000 and 7,000 metres, though – still crazy\-high.  

 




How many Himalayan peaks remain unclimbed?
------------------------------------------


Before getting into *when* peaks were first climbed, let’s look at *if* they have been climbed at all!



```
peaks %>%
  ggplot(aes(climbing_status, fill = climbing_status)) +
  geom_bar() +
  scale_fill_fish(option = "Pseudocheilinus_tetrataenia",
                  discrete = TRUE,
                  direction = -1) +
  labs(
    title = "More than a quarter of Himalayan peaks remain unclimbed",
    caption = "Source: The Himalayan Database",
    x = "",
    y = "Number of peaks"
  ) +
  theme(legend.position = "none",
        text = element_text(family = "Bahnschrift"))
```

![](opensource/tidytuesday/2020-09-22/images/1.png)


More than a quarter of them haven’t been summitted yet. I wonder why. Maybe the routes are very technically challenging, the weather is very bad, or they are very remote? I know our focus is on peaks and first ascents, but let’s see if we can find the result of expeditions that attempted to climb these unclimbed peaks. There is a `termination_reason` field in the `expeditions` table that tells us why an expedition ended.



```
peaks %>%
  filter(climbing_status == "Unclimbed") %>%
  inner_join(expeditions, by = "peak_id") %>%
  count(termination_reason) %>%
  mutate(
    # Truncating long descriptions
    termination_reason = case_when(
      str_detect(termination_reason, "Route technically") ~ "Route technically too difficult",
      str_detect(termination_reason, "Bad conditions") ~ "Bad conditions",
      TRUE ~ termination_reason
    ),
    termination_reason = fct_reorder(termination_reason, n)
  ) %>%
  ggplot(aes(n, termination_reason, fill = termination_reason)) +
  geom_col() +
  scale_fill_fish(option = "Pseudocheilinus_tetrataenia",
                  discrete = TRUE) +
  labs(
    title = "Technical routes a challenge for unclimbed peaks",
    subtitle = "Termination reasons for expeditions to unclimbed peaks",
    caption = "Source: The Himalayan Database",
    x = "Number of expeditions",
    y = ""
  ) +
  theme(legend.position = "none",
        text = element_text(family = "Bahnschrift"))
```

![](opensource/tidytuesday/2020-09-22/images/2.png)


Aha! It looks like some of our theories are borne out by the data. The top reason for expeditions to unclimbed peaks to end is the route being technically too difficult. Bad conditions and bad weather also rank pretty high.


I’m a bit concerned about the data we’re using to answer this question, though. Some expeditions are considered successes, but how can an expedition be successful and the peak still be considered unclimbed? Non\-current data is a possibility, but it’s also very likely that I’m not interpreting these fields correctly. Since this is a detour, I’ll leave this for now.  

 




When were Himalayan peaks first climbed?
----------------------------------------


Now that we have some understanding of unclimbed peaks, let’s look at those that have been climbed – specifically, *when* they were climbed.



```
peaks %>%
  ggplot(aes(first_ascent_year)) +
  geom_histogram(fill = fish(1, option = "Pseudocheilinus_tetrataenia", direction = -1),
                 alpha = 0.8) +
  theme(text = element_text(family = "Bahnschrift"))
```

![](opensource/tidytuesday/2020-09-22/images/3.png)


This is why creating a histogram is often a good idea. According to this, a small number of peaks (maybe just one) were first climbed around the year 200\. Somehow I doubt this is accurate. Fortunately, the `peaks` table has a `first_ascent_expedition_id` field, so we can look up the date of that expedition.



```
peaks %>%
  filter(first_ascent_year < 1000) %>%
  left_join(
    expeditions %>% select(expedition_id, year),
    by = c("first_ascent_expedition_id" = "expedition_id")
  ) %>%
  select(peak_name, first_ascent_year, first_ascent_expedition_id, year)
```


```
## # A tibble: 1 x 4
##   peak_name  first_ascent_year first_ascent_expedition_id  year
##   <chr>                  <dbl> <chr>                      <dbl>
## 1 Sharphu II               201 SPH218301                   2018
```

That outlier on the histogram is just one peak – Sharpu II – that is miscoded as occurring in the year 201\. The expedition is from 2018, so let’s create a new dataframe with a corrected date.



```
peaks_fixed <- peaks %>%
  mutate(first_ascent_year = ifelse(peak_id == "SPH2", 2018, first_ascent_year))
```

 


Let’s try the histogram again.



```
peaks_fixed %>%
  ggplot(aes(first_ascent_year)) +
  geom_histogram(
    binwidth = 5,
    fill = fish(1, option = "Pseudocheilinus_tetrataenia", direction = -1),
    alpha = 0.8
  ) +
  scale_x_continuous(breaks = seq(1910, 2020, 10)) +
  labs(title = "Climbers are still summitting peaks for the first time",
       subtitle = "Year of first ascent for Himalayan peaks",
       caption = "Source: The Himalayan Database",
       x = "Year of first ascent (5-year bins)",
       y = "Number of first ascents") +
  theme(text = element_text(family = "Bahnschrift"),
        panel.grid.minor = element_blank())
```

![](opensource/tidytuesday/2020-09-22/images/4.png)


Much better. There weren’t many first ascents before 1950, but after that there was a flurry of activity. For reference, Edmund Hillary and Tenzing Norgay [first summitted Mount Everest in 1953](https://en.wikipedia.org/wiki/1953_British_Mount_Everest_expedition). I wonder whether their expedition reflected a greater interest in the Himalayas or whether the expedition itself resulted in more interest.


Regardless of the answer, there have been many first ascents since 2000, which I found a bit surprising. Climbers are still accomplishing things that no one else has before. And, as we just saw, there are still many peaks the haven’t been climbed at all.  

 




Which countries were involved in first ascents?
-----------------------------------------------


I’ll admit that when I picture early climbing expeditions in the Himalayas, I imagine a bunch of Brits and Nepalese sherpas. Is this mental picture accurate, or is it a product of growing up with an Anglo\-centric education?



```
top_20_countries <- peaks_fixed %>%
  filter(!is.na(first_ascent_country)) %>%
  separate_rows(first_ascent_country, sep = ",") %>%
  mutate(
    # Get rid of whitespace after separate_rows
    first_ascent_country = str_squish(first_ascent_country),
    # Aggregate W Germany and Germany into "Germany"
    first_ascent_country = ifelse(
      first_ascent_country == "W Germany",
      "Germany",
      first_ascent_country
    )
  ) %>%
  count(first_ascent_country, name = "first_ascents", sort = TRUE) %>%
  mutate(first_ascent_country = fct_reorder(first_ascent_country, first_ascents)) %>%
  top_n(20, wt = first_ascents)

top_20_countries %>%
  ggplot(aes(first_ascents, first_ascent_country, fill = first_ascent_country)) +
  geom_col() +
  scale_x_continuous(breaks = seq(0, 150, 25)) +
  scale_fill_fish(option = "Pseudocheilinus_tetrataenia",
                  discrete = TRUE) +
  labs(
    title = "Nepal and Japan lead the way in first ascents",
    subtitle = "First ascents a country's citizen was involved in",
    caption = "Source: The Himalayan Database",
    x = "Number of first ascents",
    y = ""
  ) +
  theme(
    legend.position = "none",
    text = element_text(family = "Bahnschrift"),
    panel.grid.minor = element_blank()
  )
```

![](opensource/tidytuesday/2020-09-22/images/5.png)


The Nepalese part was right, but I had no idea Japanese climbers have been so involved in first ascents! I feel bad for having a biased mental picture, but I’m glad I’m learning new things through exploring this data.  

 


We saw above that there were two rough peaks in first ascents – one in the 1950s and 1960s and another in the 2000s and 2010s. Have the countries involved changed over time? By looking at the percentage of first ascents involving different countries’ citizens, we can answer that question. We look at percentage because we are interested in the *proportion* of ascents a country was involved in, not the absolute number. Using percentage let’s us compare decades that have different numbers of ascents.



```
countries_by_decade <- peaks_fixed %>%
  filter(!is.na(first_ascent_country),
         first_ascent_year >= 1910) %>%
  separate_rows(first_ascent_country, sep = ",") %>%
  mutate(
    first_ascent_country = str_squish(first_ascent_country),
    first_ascent_country = ifelse(
      first_ascent_country == "W Germany",
      "Germany",
      first_ascent_country
    ),
    first_ascent_decade = first_ascent_year %/% 10 * 10,
    first_ascent_country = fct_lump(first_ascent_country, 8)
  ) %>%
  count(first_ascent_country,
        first_ascent_decade,
        name = "first_ascents") %>%
  group_by(first_ascent_decade) %>%
  mutate(pct_of_ascents = first_ascents / sum(first_ascents)) %>%
  ungroup() %>%
  mutate(
    first_ascent_country = fct_reorder(first_ascent_country, -first_ascents, sum),
    first_ascent_country = fct_relevel(first_ascent_country, "Other", after = Inf)
  )

countries_by_decade %>%
  ggplot(aes(first_ascent_decade, pct_of_ascents, fill = first_ascent_country)) +
  geom_col() +
  scale_x_continuous(breaks = seq(1930, 2010, 20)) +
  scale_y_continuous(labels = percent_format(accuracy = 1)) +
  scale_fill_fish(option = "Pseudocheilinus_tetrataenia",
                  discrete = TRUE,
                  direction = -1) +
  facet_wrap( ~ first_ascent_country) +
  labs(title = "Nepal has been consistently involved in first ascents",
       subtitle = "Percent of first ascents involving a countries' citizens",
       caption = "Source: The Himalayan Database",
       x = "Decade of first ascent",
       y = "") +
  theme(text = element_text(family = "Bahnschrift"),
        legend.position = "none",
        panel.grid.major.x = element_blank(),
        panel.grid.minor = element_blank(),
        strip.text = element_text(colour = "black"),
        strip.background = element_blank())
```

![](opensource/tidytuesday/2020-09-22/images/6.png)


I see a few interesting things:


* Nepal has been fairly consistently involved in first ascents
* Japan too, though a little less so recently
* UK was involved in many early first ascents (pre\-1960\)
* US involvement has been slowly increasing since the mid\-20th century
* Switzerland was climbing mountains like gangbusters in the 1940s – maybe other countries were too involved in World War II and rebuilding afterwards?




Conclusion
----------


We’ve learned some interesting things about Himalayan peaks and some of the pioneering climbing expeditions that summitted those peaks for the first time. I don’t any more than the average person about mountain climbing, though, so please take this as what it is: the exploration of a non\-expert. If you enjoyed this post, [let me know](https://twitter.com/alexcookson) on Twitter and consider reading *Part 2* of this series, which [looks at how dangerous it is to climb Everest](https://www.alexcookson.com/post/how-dangerous-is-climbing-mount-everest/) (and other questions).









[Mapping San Francisco's trees](https://alexcookson.com/post/mapping-san-francisco-trees/)



  
 


[How dangerous is climbing Mount Everest?](https://alexcookson.com/post/how-dangerous-is-climbing-mount-everest/)

















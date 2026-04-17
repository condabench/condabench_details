Scraping London Marathon data with {rvest} \| Nicola Rennie
This website uses Google Analytics to improve its functionality.  
  
Accept
Deny[About](/ "About")
[Projects](/projects/ "Projects")
[Talks](/talks/ "Talks")
[Blog](/blog/ "Blog")
[Links](/links/ "Links")
Scraping London Marathon data with {rvest}
==========================================

{rvest} is an R package within the {tidyverse} which helps you scrape data from web pages. This blog post will showcase an example of scraping data from Wikipedia on London Marathon races and winners.

March 16, 2023

There are lots of ways to get data into R: reading from local files or URLs, R packages containing data, using packages that wrap APIs, to name a few. But sometimes, none of those are an option. Let’s say you want get a table of data from a website (that doesn’t provide API access). You *could* copy and paste it into a spreadsheet, re\-format it manually, and then read it into R. But (to me, at least) that sounds horribly tedious\&mldr;

That’s where {rvest} comes in. {rvest} is an R package within the {tidyverse} which helps you scrape data from web pages. This blog post will showcase an example of scraping data from Wikipedia on London Marathon races and winners. By the end, you should be ready to scrape some data of your own!

  
Image: [giphy.com](https://giphy.com/gifs/muppets-LmBsnpDCuturMhtLfw)


> A note on web\-scraping: many websites have a `robots.txt` file which contains instructions for bots that tell them which webpages they can and cannot access. The relies on voluntary compliance, so please check a websites `robots.txt` file before you jump straight to web\-scraping. If you’re scraping multiple pages, you can use the
> [{polite}](https://dmi3kno.github.io/polite/) package to make sure you respect the `robots.txt` file.

Loading the R packages
----------------------

For the process of scraping the London Marathon data from
[Wikipedia](https://en.wikipedia.org/wiki/List_of_winners_of_the_London_Marathon), we need five R packages: {rvest} for web\-scraping, {dplyr} for manipulating the scraped data, {lubridate} and {chron} for working with the time data (optional depending on your use case), and {readr} to save the data for re\-use later.



| ``` 1 2 3 4 5  ``` | ``` library(rvest) library(dplyr) library(lubridate) library(chron) library(readr)  ``` |
| --- | --- |

Scraping the data
-----------------

Now let’s actually get the data! The key function in {rvest} is `read_html()` which does what it says on the tin and reads in the HTML code used on the site you pass in as the first argument:



| ``` 1 2 3  ``` | ``` london <- read_html(   "https://en.wikipedia.org/wiki/List_of_winners_of_the_London_Marathon"   )  ``` |
| --- | --- |

The initial output doesn’t look particularly nice:



| ``` 1 2 3 4  ``` | ``` {html_document} <html class="client-nojs vector-feature-language-in-header-enabled vector-feature-language-in-main-page-header-disabled vector-feature-language-alert-in-sidebar-enabled vector-feature-sticky-header-disabled vector-feature-page-tools-disabled vector-feature-page-tools-pinned-disabled vector-feature-main-menu-pinned-disabled vector-feature-limited-width-enabled vector-feature-limited-width-content-enabled" lang="en" dir="ltr"> [1] <head>\n<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">\n<meta charset="UTF-8"> ... [2] <body class="skin-vector skin-vector-search-vue vector-toc-pinned mediawiki ltr sitedir-ltr mw-hide ...  ``` |
| --- | --- |

Fortunately, {rvest} has some nice functions to parse this output for you, and get the elements of the site that you’re actually interested in.



| ``` 1 2 3  ``` | ``` london <- london %>%    html_elements(".wikitable.sortable") %>%    html_table()  ``` |
| --- | --- |

Here, I’ve passed in `".wikitable.sortable"` to `html_elements()`. Here, `html_elements()` grabs all the elements which have `".wikitable.sortable"` as their CSS class. I determined that `".wikitable.sortable"` was the class I was looking for by using `Inspect` on the Wikipedia page (use the Ctrl \+ Shift \+ I shortcut). The `html_table()` then tidies this up even further, and returns a list of tibbles where each list entry is a different table from the Wikipedia page.

Tidying it up
-------------

The first four tibbles contain information on the four categories of racing at London Marathon, and the fifth contains a summary table by country. Since the fifth table data can be captured from the first four, and it’s in a completely different format, I decided to discard it. Now what I want to do is combine the remaining four tibbles into a single tibble, with an additional column determining which race the data relates to.

First things first, let’s decide what the names of the categories are. I *could* have grabbed this information from the Wikipedia itself, as each table has a section header. However, the title’s weren’t quite what I was looking for and I would have had to recode them anyway, so I decided to just directly *recode* the list of tibbles. The categories can then be set as the names of the list items.



| ``` 1 2 3  ``` | ``` london <- london[1:4]  categories <- c("Men", "Women", "Wheelchair Men", "Wheelchair Women") names(london) <- categories  ``` |
| --- | --- |

Fortunately for me, the column names in the four remaining tables already all have the same names. This meant I could take advantage of `bind_rows()` from {dplyr} to collapse the list into a single tibble. Setting `.id = "Category"` creates a new column in the tibble called `Category` which contains the list name as a variable. I also dropped the `Notes` free text column.



| ``` 1 2  ``` | ``` london <- bind_rows(london, .id = "Category") %>%    select(-Notes)  ``` |
| --- | --- |

The last bit of processing to do is deal with the time data. I decided to rename the column to `Time`, and convert it to a formal time object using the `chron()` function from {chron}. The `Year` column was slightly trickier than it appeared at first glance \- some of the entries had a footnote marker next to the year \- so `as.numeric()` doesn’t work out of the box, it needed a little regex first!



| ``` 1 2 3 4 5  ``` | ``` winners <- london %>%    rename(Time = `Time(h:m:s)`) %>%    mutate(Time = chron(times = Time)) %>%    mutate(Year = gsub("\\[|*.\\]", "", Year),           Year = as.numeric(Year)) %>%   ``` |
| --- | --- |

Finally, we can save the data, either as a CSV or an RDS file to make it easier to work with it later, and to avoid repeatedly scraping the same data.



| ``` 1 2  ``` | ``` write_csv(winners, file = "winners.csv") saveRDS(winners, file = "winners.rds")  ``` |
| --- | --- |

Repeating the process
---------------------

I decided to repeat the process for data on number of London Marathon participants, and how much charity money was raised, as this might pose some interesting questions for further analysis. You can see here, that the process is quite similar:



| ```  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22  ``` | ``` # grab table of data with notes london_data <- read_html("https://en.wikipedia.org/wiki/London_Marathon") london_data <- london_data %>%    html_elements(".wikitable.sortable") %>%    html_table()  # convert columns to correct type london_marathon <- london_data[[1]] %>%    select(-Edition) %>%    mutate(Date = dmy(Date)) %>%    mutate(Year = year(Date), .after = 1) %>%    rename(Raised = `Charity raised(£ millions)`) %>%    mutate(Raised = gsub("\\[|*.\\]", "", Raised),           Raised = as.numeric(Raised)) %>%    mutate(across(c(Applicants, Accepted, Starters, Finishers), parse_number)) %>%    mutate(`Official charity` = case_when(`Official charity` == "—" ~ NA_character_,                                         `Official charity` == "" ~ NA_character_,                                         TRUE ~ `Official charity`))  # save as csv write_csv(london_marathon, file = "london_marathon.csv") saveRDS(london_marathon, file = "london_marathon.rds")  ``` |
| --- | --- |

Working with the data
---------------------

Now, we can work with the scraped data in the same way we’d work with any other (cleaned up) data in R! Including making plots!

![Barchart of London Marathon winners by country](opensource/tidytuesday/2023-04-25/images/0.png)
![Dumbbell chart of London marathon starters and finishers](opensource/tidytuesday/2023-04-25/images/1.png)

Code for the plots can be found on
[GitHub](https://github.com/nrennie/LondonMarathon/blob/main/inst/plots.R).

If you’re only interested in working with the data, and less in the web scraping, you can load the data directly from the
[{LondonMarathon}](https://github.com/nrennie/LondonMarathon) R package with:



| ``` 1 2 3  ``` | ``` remotes::install_github("nrennie/LondonMarathon") data(winners, package = "LondonMarathon") data(london_marathon, package = "LondonMarathon")  ``` |
| --- | --- |

Final thoughts
--------------

I hope this blog post has convinced you that scraping data from a website does need to be as difficult as it sounds, and that it’s a better option that copying and pasting! The code, data, data dictionary, and a few exploratory plots can be found on
[GitHub](https://github.com/nrennie/LondonMarathon).

If you need to interact with the website you’re scraping in some way e.g. inputting log in details, or clicking on buttons to select data, you’ll likely find
[{RSelenium}](https://docs.ropensci.org/RSelenium/) a very useful package! This
[blog post](http://brooksandrew.github.io/simpleblog/articles/scraping-with-selenium/) from
[Andrew Brooks](https://github.com/brooksandrew) on how to use {RSelenium} for web scraping gives a short introduction.

The background photo in the cover image of this blog post is from
[Benjamin Davies](https://unsplash.com/@bendavisual) on
[Unsplash](https://unsplash.com/photos/Oja2ty_9ZLM).



---

For attribution, please cite this work as:


> **Scraping London Marathon data with {rvest}**.  
> Nicola Rennie. March 16, 2023\.  
> [nrennie.rbind.io/blog/web\-scraping\-rvest\-london\-marathon](https://nrennie.rbind.io/blog/web-scraping-rvest-london-marathon)

BibLaTeX Citation
```

@online{rennie2023,
  author = {Nicola Rennie},
  title = {Scraping London Marathon data with {rvest}},
  date = {2023-03-16},
  url = {https://nrennie.rbind.io/blog/web-scraping-rvest-london-marathon}
}

```
Licence: [creativecommons.org/licenses/by/4\.0](https://creativecommons.org/licenses/by/4.0/)

[← Seeing double? Building the same app in Shiny for R and Shiny for Python](https://nrennie.rbind.io/blog/seeing-double-shiny-python-r/)
[Detecting heart murmurs from time series data in R →](https://nrennie.rbind.io/blog/detecting-heart-murmurs-time-series-r-tidymodels/)On this page
------------

* [Loading the R packages](#loading-the-r-packages)
* [Scraping the data](#scraping-the-data)
* [Tidying it up](#tidying-it-up)
* [Repeating the process](#repeating-the-process)
* [Working with the data](#working-with-the-data)
* [Final thoughts](#final-thoughts)


---

© 2024 Nicola Rennie. Made with [Hugo Apéro](https://github.com/hugo-apero/).


Data Visualization in the Tidyverse









class: center, middle, inverse, title\-slide

\# Data Visualization in the Tidyverse
\#\# The Great Tidy Plot Off
\#\#\# Alison Hill, PhD   
 Data Scientist \& Professional Educator   
  
 [apreshill](https://github.com/apreshill)  
  [@apreshill](https://twitter.com/apreshill)  
 [alison@rstudio.com](mailto:alison@rstudio.com)  


\-\-\-





class: center, middle, inverse

\# Inspired by:

\#\# \[Flowing Data: One Dataset Visualized 25 Ways](https://flowingdata.com/2017/01/24/one\-dataset\-visualized\-25\-ways/)

\<img src\="img/flowing\-data\-inspo.png" width\="70%" style\="display: block; margin: auto;" /\>


\-\-\-
class: center, middle, inverse

\#\# Disclaimers

\-\-

I am a data visualization .whisper\[practioner]. 

\-\-

I offer what I hope are well\-reasoned opinions here, but obviously .whisper\[YMMV].

\-\-

I do not claim that all of the following are .whisper\[good] nor .whisper\[publication\-worthy] visualizations (for those viewing these slides without narrative)

!\[](https://media.giphy.com/media/3oEjHIs0EQ4nxN4YPC/giphy.gif)

\-\-\-
class:middle, inverse, center

\#\# My messages for today

\-\-\-
class:middle, inverse, center

\#\# tidiness \`\\(\\neq\\)\` .shout\[godliness]

!\[](https://media.giphy.com/media/3o6vXSvvyxyzJMVqGk/giphy.gif)

\-\-\-
class:middle, inverse, center

\#\# tidiness \= .whisper\[nimbleness]

!\[](https://media.giphy.com/media/3o7TKFVl2L6P6P7zqM/giphy.gif)

\-\-\-
class:middle, inverse, center

\#\# tidy \`\\(\\neq\\)\` .shout\[done]

!\[](https://media.giphy.com/media/l41YtBXZvSRdgqq7m/giphy.gif)

\-\-\-
class:middle, inverse, center

\<img src\="img/tidyverse\_wrangle.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
class: center, middle, inverse

\#\# But also...

Don't be afraid to chop out those \`ggplot2\` defaults! 

!\[](https://media.giphy.com/media/26BoDD0vgBWAipgJ2/giphy.gif)

\-\-\-
class: center, middle, inverse

\#\# But also...

It's all in the details.

!\[](https://media.giphy.com/media/l0MYrsYIulHYo0Bhe/giphy.gif)

\-\-\-
\# Packages first

I'll use all of the following:


\`\`\`r
library(tidyverse)
library(bakeoff) \# data \+ colors!
\`\`\`

\-\-\-
\# Data second


\`\`\`r
ratings \<\- ratings\_seasons %\>% 
 mutate(series \= as.factor(series))
\`\`\`

\-\-\-
\# Glimpse


\`\`\`
Observations: 74
Variables: 10
$ series \<fct\> 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2,...
$ episode \<int\> 1, 2, 3, 4, 5, 6, 1, 2, 3, 4, 5, 6, 7, 8,...
$ uk\_airdate \<date\> 2010\-08\-17, 2010\-08\-24, 2010\-08\-31, 2010\...
\*$ viewers\_7day \<dbl\> 2\.24, 3\.00, 3\.00, 2\.60, 3\.03, 2\.75, 3\.10,...
$ viewers\_28day \<dbl\> 7, 3, 2, 4, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1,...
$ network\_rank \<int\> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N...
$ channels\_rank \<int\> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N...
$ bbc\_iplayer\_requests \<dbl\> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N...
$ us\_season \<int\> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N...
$ us\_airdate \<date\> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, ...
\`\`\`


\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 1: Continuous Bar Chart

\-\-\-
\#\# Recipe 1: Continuous Bar Chart

\<img src\="index\_files/figure\-html/episodebar\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 1: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geom]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/episodebar\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]

\-\-\-
\#\# Recipe 1: Code for Bar Chart


\`\`\`r
\# create continuous episode count
plot\_off1 \<\- ratings %\>% 
\* mutate(ep\_id \= row\_number()) %\>%
 select(ep\_id, viewers\_7day, series, episode)

\# create coordinates for labels
series\_labels \<\- plot\_off1 %\>% 
 group\_by(series) %\>% 
 summarize(y\_position \= median(viewers\_7day) \+ 1,
 x\_position \= mean(ep\_id))

\# make the plot
\*ggplot(plot\_off1, aes(x \= ep\_id, y \= viewers\_7day, fill \= series)) \+
\* geom\_col(alpha \= .9\) \+
 ggtitle("Series 8 was a Big Setback in Viewers",
 subtitle\= "7\-Day Viewers across All Series/Episodes") \+
 geom\_text(data \= series\_labels, aes(label \= series,
 x \= x\_position, 
 y \= y\_position)) \+
 theme(axis.text.x \= element\_blank(),
 axis.ticks.x \= element\_blank(),
 axis.title.x \= element\_blank(),
 panel.grid.major.x \= element\_blank(),
 panel.grid.minor.x \= element\_blank()) \+ 
 scale\_fill\_bakeoff(guide \= FALSE) \+
 scale\_x\_continuous(expand \= c(0, 0\)) 
\`\`\`

\-\-\-
class: center, middle, inverse

\# 🍰

\#\# What is going on with Series 8?

\> \*"The eighth series of The Great British Bake Off began on 29 August 2017, with this being the first of The Great British Bake Off to be broadcast on Channel 4, after the production company Love Productions moved the show. It is the first series for new hosts Noel Fielding and Sandi Toksvig, and new judge Prue Leith." \-\- \<a href\="https://en.wikipedia.org/wiki/The\_Great\_British\_Bake\_Off\_(series\_8\)"\>Wikipedia\</a\>\*

\-\-\-
class: center, middle, inverse

!\[](https://media.giphy.com/media/l0HlLycAY0hSUtiYo/source.gif)

\#\# Read: 

\-\-

\#\# No Mary Berry, no Mel, no Sue

\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 2: Lollipop Plot

\-\-\-

\#\# Recipe 2: Lollipop Plot

\<img src\="index\_files/figure\-html/lolli\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 2: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[3 geoms]?
1\. What .whisper\[variable] is .shout\[facet wrapped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/lolli\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-

\#\# Recipe 2: Code for Lollipop Plot


\`\`\`r
plot\_off2 \<\- ratings %\>% 
\* group\_by(series) %\>%
\* mutate(series\_avg \= mean(viewers\_7day, na.rm \= TRUE),
\* diff\_avg \= viewers\_7day \- series\_avg) %\>%
 filter(max(episode) \=\= 10\) %\>% 
 mutate(episode \= as.factor(episode)) %\>% 
 select(episode, viewers\_7day, series, diff\_avg, series\_avg)

\*ggplot(plot\_off2, aes(x \= episode, y \= viewers\_7day, color \= diff\_avg)) \+
\* geom\_hline(aes(yintercept \= series\_avg), alpha \= .5\) \+
\* geom\_point() \+
\* geom\_segment(aes(xend \= episode, yend \= series\_avg)) \+
\* facet\_wrap(\~series) \+
 scale\_color\_viridis\_c(option\="plasma", begin \= 0, 
 end \= .8, guide \= FALSE) \+
 ggtitle("Great British Bake Off Finales Get the Most Viewers",
 subtitle \= "Way Higher than Series Average (for Series with 10 episodes)")
\`\`\`



\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 3: Series Line Plot

\-\-\-
\#\# Recipe 3: Series Line Plot

\<img src\="index\_files/figure\-html/serieslines\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 3: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geom]?
1\. What .whisper\[variable] is .shout\[grouped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/serieslines\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 3: Code for Series Line Plot


\`\`\`r
line\_labels \<\- ratings %\>% 
 group\_by(series) %\>% 
 filter(episode \=\= max(episode)) %\>% 
 select(series, x\_position \= episode, y\_position \= viewers\_7day)

\*ggplot(ratings, aes(x \= as.factor(episode),
\* y \= viewers\_7day,
\* color \= as.factor(series),
\* group \= series)) \+
\* geom\_line() \+
 scale\_color\_bakeoff(guide \= FALSE) \+
 labs(color \= "Series", x \= "Episode") \+
 geom\_text(data \= line\_labels, aes(label \= series,
 x \= x\_position \+ .25, 
 y \= y\_position)) 
\`\`\`


\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 4: Facetted Line Plot

\-\-\-
\#\# Recipe 4: Facetted Line Plot

\<img src\="index\_files/figure\-html/facetlines\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 4: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geom]?
1\. What .whisper\[variable] is .shout\[facetted]?
1\. What .whisper\[variable] is .shout\[grouped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/facetlines\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 4: Code for Facetted Line Plot


\`\`\`r
\*ggplot(ratings, aes(x \= as.factor(episode),
\* y \= viewers\_7day,
\* color \= fct\_reorder2(series, episode, viewers\_7day),
\* group \= series)) \+
\* facet\_wrap(\~series) \+
\* geom\_line(lwd \= 2\) \+
 scale\_color\_bakeoff(guide \= FALSE) \+
 labs(color \= "Series", x \= "Episode") 
\`\`\`

\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 5: First vs. Last

\-\-\-
\#\# Recipe 5: First vs. Last

\<img src\="index\_files/figure\-html/firstlastline\-1\.png" width\="60%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 5: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geoms]?
1\. What .whisper\[variable] is .shout\[grouped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/firstlastline\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 5: Code for First vs. Last


\`\`\`r
\# some wrangling here
plot\_off5 \<\- ratings %\>% 
 select(series, episode, viewers\_7day) %\>% 
\* group\_by(series) %\>%
\* filter(episode \=\= 1 \| episode \=\= max(episode)) %\>%
\* mutate(episode \= recode(episode, \`1\` \= "first", .default \= "last")) %\>%
 ungroup()

\# code for plot
\*ggplot(plot\_off5, aes(x \= series,
\* y \= viewers\_7day,
\* color \= fct\_reorder2(episode, series, viewers\_7day),
\* group \= episode)) \+
\* geom\_point() \+
\* geom\_line() \+
 scale\_color\_bakeoff() \+
 ggtitle("Great British Bake Off Finales Get More Viewers than Premieres") \+
 labs(color \= "Episode")
\`\`\`

\-\-\-
class: center, middle, inverse

\# 🍰

\#\# What is going on with the Series 8 finale?

\-\-\-
class: middle, center, inverse

\#\# A \[tweet](https://twitter.com/PrueLeith/status/925329937644564480\) heard 'round the world

\<blockquote class\="twitter\-tweet" data\-lang\="en"\>\<p lang\="en" dir\="ltr"\>I am so sorry to the fans of the show for my mistake this morning, I am in a different time zone and mortified by my error \<a href\="https://twitter.com/hashtag/GBBO?src\=hash\&amp;ref\_src\=twsrc%5Etfw"\>\#GBBO\</a\>.\</p\>\&mdash; Prue Leith (@PrueLeith) \<a href\="https://twitter.com/PrueLeith/status/925329937644564480?ref\_src\=twsrc%5Etfw"\>October 31, 2017\</a\>\</blockquote\>




\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 6: Dumbbell Plot

\-\-\-
\#\# Recipe 6: Dumbbell Plot


\<img src\="index\_files/figure\-html/dumbbell\-1\.png" width\="60%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 6: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geoms]?
1\. What .whisper\[variable] is .shout\[grouped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/dumbbell\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 6: Code for Dumbbell Plot



\`\`\`r
\*ggplot(plot\_off5, aes(x \= viewers\_7day,
\* y \= fct\_rev(series),
\* color \= episode,
\* group \= series)) \+
\* geom\_line(size \= .75\) \+
\* geom\_point(size \= 2\.5\) \+
 scale\_color\_bakeoff() \+
 labs(y \= "Series", x \= "Viewers (millions)", color \= "Episode") \+
 ggtitle("Great British Bake Off Finales Get More Viewers than Premieres") 
\`\`\`

\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 7: Slope Graph

\-\-\-
\#\# Recipe 7: Slope Graph 


\<img src\="index\_files/figure\-html/slope\-1\.png" width\="65%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 7: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geoms]?
1\. What .whisper\[variable] is .shout\[grouped]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/slope\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 7: Code for Slope Graph


\`\`\`r
slope\_labels \<\- plot\_off5 %\>% 
 filter(episode \=\= "last") %\>% 
 select(series, x\_position \= episode, y\_position \= viewers\_7day)

\*ggplot(plot\_off5, aes(x \= episode,
\* y \= viewers\_7day,
\* color \= series,
\* group \= series)) \+
\* geom\_point() \+
\* geom\_line() \+
 scale\_color\_bakeoff(guide \= FALSE) \+
 geom\_text(data \= slope\_labels, aes(label \= series,
 x \= x\_position,
 y \= y\_position),
 nudge\_x \= .1\) \+
 theme(panel.grid \= element\_blank(),
 axis.line \= element\_line(color \= "gray"))
\`\`\`


\-\-\-
class: center, middle, inverse

\# 🍰


\#\# Recipe 8: Finale "Bumps"

\-\-\-
\#\# Recipe 8: Finale "Bumps"

\<img src\="index\_files/figure\-html/bump\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 8: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geom]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/bump\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 8: Code for Finale "Bumps"


\`\`\`r
\# some more serious wrangling here
plot\_off8 \<\- ratings %\>% 
 select(series, episode, viewers\_7day) %\>% 
 group\_by(series) %\>% 
 filter(episode \=\= 1 \| episode \=\= max(episode)) %\>% 
\* mutate(episode \= recode(episode, \`1\` \= "first", .default \= "last")) %\>%
\* spread(episode, viewers\_7day) %\>%
\* mutate(finale\_bump \= last \- first)

\# plot
\*ggplot(plot\_off8, aes(x \= fct\_rev(series),
\* y \= finale\_bump)) \+
\* geom\_col(fill \= bakeoff\_cols("baltic"), alpha \= .7\) \+
\* coord\_flip() \+
 labs(x \= "Series", y \= "Difference in Viewers for Finale from Premiere (millions)") \+
 ggtitle("Finale 'Bumps' were Smallest for Series 1 and 8",
 subtitle \= "Finale 7\-day Viewers Relative to Premiere")
\`\`\`



\-\-\-
class: center, middle, inverse

\# 🍰

\#\# Recipe 9: % Change Bar Chart

\-\-\-
\#\# Recipe 9: % Change Bar Chart

\<img src\="index\_files/figure\-html/changebar\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 9: Questions

.left\-column\[
1\. Which .whisper\[dataset]?
1\. Which .whisper\[geom]?
1\. What .whisper\[variable] is mapped on the .shout\[x\-axis]?
1\. What .whisper\[variable] is mapped on the .shout\[y\-axis]?
1\. What .whisper\[variable] is mapped to .shout\[color]?
]

.right\-column\[
\<img src\="index\_files/figure\-html/changebar\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>
]
\-\-\-
\#\# Recipe 9: Code for % Bar


\`\`\`r
\# wrangling to calculate percent change
plot\_off9 \<\- ratings %\>% 
 select(series, episode, viewers\_7day) %\>% 
 group\_by(series) %\>% 
 filter(episode \=\= 1 \| episode \=\= max(episode)) %\>% 
 ungroup() %\>% 
 mutate(episode \= recode(episode, \`1\` \= "first", .default \= "last")) %\>% 
\* spread(episode, viewers\_7day) %\>%
\* mutate(pct\_change \= (last \- first) / first)

\# plot
\*ggplot(plot\_off9, aes(x \= fct\_rev(series),
\* y \= pct\_change)) \+
\* geom\_col(fill \= bakeoff\_cols("baltic"), alpha \= .5\) \+
 geom\_hline(aes(yintercept \= median(pct\_change, na.rm \= TRUE)), 
 color \= bakeoff\_cols("berry"),
 lwd \= 2\) \+
 labs(x \= "Series", y \= "% Increase in Viewers, First to Last Episode") \+
 ggtitle("Series 8 had a 6% Increase in Viewers from Premiere to Finale",
 subtitle\= "The Lowest Across All Series (Line is the Median)") \+ 
 scale\_y\_continuous(labels \= scales::percent) \+
 coord\_flip() 
\`\`\`


\-\-\-
class: center, middle, inverse

\# 🎂

\#\# Recipe 10: Lollipop Plot, % Change

\-\-\-
\#\# Recipe 10: Lollipop Plot, % Change

\<img src\="index\_files/figure\-html/lollipercent\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 10: Code for % Lollipop Plot


\`\`\`r
\# plot
\*ggplot(plot\_off9, aes(x \= fct\_rev(series),
\* y \= pct\_change)) \+
\* geom\_point(color \= bakeoff\_cols("bluesapphire"), size \= 2\) \+
\* geom\_segment(aes(xend \= fct\_rev(series), yend \= 0\), color \= bakeoff\_cols("bluesapphire")) \+
 geom\_text(aes(label \= scales::percent(pct\_change)), hjust \= \-.25\) \+
 labs(x \= "Series", y \= "% Change in Viewers from First to Last Episode") \+
 ggtitle("Percent Increase in Viewers was the Smallest for Series 8",
 subtitle\= "Finale 7\-day Viewers Relative to Premiere") \+
 scale\_y\_continuous(labels \= scales::percent, limits \= c(0, .85\)) \+
 coord\_flip() 
\`\`\`

\-\-\-
class: center, middle, inverse

!\[](https://media.giphy.com/media/3o6ZtgKA92iX0oT2uI/source.gif)
\-\-\-
class: center, middle, inverse

\# 🎂

\#\# Recipe 11: Scatterplot

\-\-\-
\#\# Recipe 11: Scatterplot

\<img src\="index\_files/figure\-html/scatter\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 11: Code for Scatterplot


\`\`\`r
\*ggplot(plot\_off8, aes(x \= first, y \= last)) \+
\* geom\_point() \+
\* geom\_smooth(se \= FALSE, color \= '\#EBBFDD') \+
\* geom\_abline(slope \= 1, intercept \= 0, color \= "gray", alpha \= .5\) \+
 geom\_text(aes(label \= series), hjust \= \-1\) \+
 labs(x \= "Premiere Episode 7\-day Viewers (millions)",
 y \= "Finale Episode 7\-day Viewers (millions)") \+
 coord\_equal(ratio\=1\)
\`\`\`

\-\-\-
class: center, middle, inverse

\# 🎂

\#\# Recipe 11\.1: Pop\-Out Scatterplot

\-\-\-
\#\# Recipe 11\.1: Pop\-Out Scatterplot

\<img src\="index\_files/figure\-html/lollipop\-1\.png" width\="70%" style\="display: block; margin: auto;" /\>

\-\-\-
\#\# Recipe 11\.1: Code for Pop\-Out Scatterplot


\`\`\`r
ggplot(plot\_off8, aes(x \= first, y \= last)) \+
 geom\_abline(slope \= 1, intercept \= 0, color \= "gray", alpha \= .5\) \+
 geom\_smooth(se \= FALSE, color \= "\#11B2E8") \+
 geom\_point(data \= filter(plot\_off8, series %in% c(1:7\))) \+
 geom\_point(data \= filter(plot\_off8, series \=\= 8\), colour \= "\#CF2154") \+
 geom\_text(data \= filter(plot\_off8, series %in% c(1:7\)),
 aes(label \= series), hjust \= \-1\) \+
 geom\_text(data \= filter(plot\_off8, series \=\= 8\),
 aes(label \= series), hjust \= \-1, colour \= "\#CF2154") \+
 labs(x \= "Premiere Episode 7\-day Viewers (millions)",
 y \= "Finale Episode 7\-day Viewers (millions)")
\`\`\`

\-\-\-
class:inverse, middle, center

!\[](https://media.giphy.com/media/d8m7wQHB3Ct5S/giphy.gif)
 









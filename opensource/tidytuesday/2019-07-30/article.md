




Which PC Video Games Have Endured the Test of Time? – The Cruise of Dimensionality





























































































  









[Skip to content](#content)


 [The Cruise of Dimensionality](https://cruiseofdimensionality.home.blog/)


And Other Adventures In Data Science






 Menu 
* [Home](/)
* [Contact](https://cruiseofdimensionality.home.blog/contact/)
* [About Us](https://cruiseofdimensionality.home.blog/about-us/)
* [Cruise or Curse?](https://cruiseofdimensionality.home.blog/cruise-or-curse/)
 






Which PC Video Games Have Endured the Test of Time?
===================================================

 
![Chart of five year old top selling PC Games still being played in 2019](opensource/tidytuesday/2019-07-30/images/5.png) 

[July 24, 2019July 29, 2019](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/) \~ [Liza Wood](https://cruiseofdimensionality.home.blog/author/socketbulbs/) 


As a former video game producer married to a hard\-core gamer, video games are a part of our everyday household conversation. Last week, we wondered what old PC video games are still loved and being played today. Thanks to platforms like [Steam](https://store.steampowered.com) and [GOG](https://www.gog.com), we can still buy and play our favourite games fifteen or even more years after they were originally released. Steam collects and reports a lot of user data through its web API, which is automatically gathered and presented by [Steam Spy](https://steamspy.com).  So, I downloaded Steam Spy’s free data by release year to see if it could answer our question.


Years With More Games Still Being Played
----------------------------------------


After compiling the yearly spreadsheets into a single tibble in R, I had a list of 26,678 games spanning from 2004 to 2018\. After tidying the data using the [tidyverse](https://www.tidyverse.org) tools, I first graphed the number of games released each year to get a sense of the growth of the number of games available on Steam. Next, I graphed the number of games played in the last two weeks, by the year they were released. By putting the two plots side\-by\-side, I looked for years where the number of games still being played was higher than the trend of games being released.


![Chart of PC Games on Steam By Release Year](opensource/tidytuesday/2019-07-30/images/1.png)


2004, 2009 and 2012 caught my attention. Relative to the number of games released those years, more were still being played in July 2019\. What games from those years are being played? How long are they being played?


The Steam Spy data reports the average and median length of time a game was played in the past two weeks. To ensure I was looking at data that was averaged over a large enough audience, I charted the average play times of games that had at least one million owners for each release year.


![Chart of PC Games from 2004 played in 2019](opensource/tidytuesday/2019-07-30/images/2.png)


![Graph of PC games from 2009 played in 2019](opensource/tidytuesday/2019-07-30/images/3.png)


![Chart of PC games from 2012 played in 2019](opensource/tidytuesday/2019-07-30/images/4.png)


For all three years, the most popular games for that year are still being played. Still, there are less popular games showing up for each year. The average play time for *Alan Wake* is remarkable. It has a lot of replay value for its owners after nine years. *Counter\-Strike: Global Offensive*the second highest average play time across the three years. It was one of the top five highest selling games on Steam across all the years.


Games Over 5 Years Old Played More Than 1\-2 Hours
--------------------------------------------------


I then took a look at games that were at least five years old across multiple years, comparing games with a similar number of owners. I also wondered whether there was any relation with the [Metascore](https://www.metacritic.com/about-metascores) for the game. Metascore is a weighted average of critical reviews and is considered an indication of quality.


![Chart of five year old top selling PC Games still being played in 2019](opensource/tidytuesday/2019-07-30/images/5.png)


[*DOTA2*](http://blog.dota2.com/?l=english) is the top\-owned game on Steam. It’s free\-to\-play and is a popular e\-sports game with annual international stadium\-filling tournaments.  All the games shown above have a 70\+ Metascore, indicating that they generally had favourable reviews. Garry’s Mod was not a commercially published game, so it was not critically reviewed. It is an independent modification of Half\-Life 2\. Both Garry’s Mod and Half\-Life 2 are still being played nearly 15 years after release.


![Charting showing Company of Heroes 2 was a popular old PC game played in July 2019](opensource/tidytuesday/2019-07-30/images/6.png)


*Company of Heroes 2* is currently being offered at 80% off of its usual price, which may explain its remarkably high play time in this group. The range of Metascores is also lower in this group.


For the above two charts, the games shown had an average play time of at least one hour. For the next two charts, the average was increased to two hours since there are more than four times the number of games in those groups.


![Charts showing Alan Wake and Alien Swarm with highest play time in July 2019](opensource/tidytuesday/2019-07-30/images/7.png)


The range of Metascores is wider than the previous two charts. *Alien Swarm*is a free\-to\-play game that was originally released in 2010\. Valve, the developers and publishers of the game, also released the complete code base, allowing players to make their own modifications to the game. *The Sims 3* is the only version of *The Sims* available on Steam. It’s successor is only available on the publisher’s website.


![Chart showing old PC games with 1M owners played in July 2019](opensource/tidytuesday/2019-07-30/images/8.png)


This chart has five games with no Metascore. *Mount and Blade*was released in 2008 with mixed to average reviews. Its fans have made a number of well\-knowns mods, which may give it its replay value. *S.T.A.L.K.E.R: Shadow of Chernobyl* was released in 2007 with generally favourable reviews. A sequel was announced last year, likely renewing interest.


What Was The Most Surprising?
-----------------------------


Of all the games that appeared on the above charts, the average play time for *Alan Wake* was the most surprising. It was moderately successful game with a respectable Metascore. It is not a strategy, esports or multiplayer first person shooter game, which are often played for years after initial release. Many of the other games on the charts are in these categories. It wasn’t released with mod tools, so players are not commonly customizing the game. It wasn’t on sale. According to [PC Gamer](https://www.pcgamer.com/remedy-still-wants-to-make-alan-wake-2-someday/), it was simply a game with “… interesting characters, weird story (and) beloved by fans”.


##### Resources:


* [Original data source](https://steamspy.com/year/) on Steam Spy
* [Code used for analysis and visualization](https://github.com/lizawood/apps-and-games/blob/master/PC_Games/PC_Games_Nostalgia.R)
* [Games on Metacritic](https://www.metacritic.com/game)


 




 
### Share this:

* [Click to share on LinkedIn (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=linkedin "Click to share on LinkedIn")
* [Click to share on Twitter (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=twitter "Click to share on Twitter")
* [Click to share on Facebook (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=facebook "Click to share on Facebook")
* [Click to share on Reddit (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=reddit "Click to share on Reddit")
* [Click to share on Pocket (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=pocket "Click to share on Pocket")
* [More](#)
* 

* [Click to share on WhatsApp (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/?share=jetpack-whatsapp "Click to share on WhatsApp")
* [Click to email a link to a friend (Opens in new window)](mailto:?subject=%5BShared%20Post%5D%20Which%20PC%20Video%20Games%20Have%20Endured%20the%20Test%20of%20Time%3F&body=https%3A%2F%2Fcruiseofdimensionality.home.blog%2F2019%2F07%2F24%2Fpc-video-games-we-still-play%2F&share=email "Click to email a link to a friend")
* [Click to print (Opens in new window)](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/#print "Click to print")
* 
Like Loading...

### *Related*


 


[\#TidyTuesday](https://cruiseofdimensionality.home.blog/tag/tidytuesday/)[video games](https://cruiseofdimensionality.home.blog/tag/video-games/)[visualization](https://cruiseofdimensionality.home.blog/tag/visualization/) 



 

Published by Liza Wood
----------------------




 After a dozen years leading video game development projects in a variety of roles, I decided to pursue a Master of Data Science at the University of British Columbia. Studying data science doesn’t mean I’m moving away from leading people. Growing data science teams need collaborative, pragmatic, Agile leadership to connect data to all areas of the business. I would like to share that point of view, along with my experiences, on this blog. [View all posts by Liza Wood](https://cruiseofdimensionality.home.blog/author/socketbulbs/) 






Post navigation
---------------


[‹ PreviousThe Great Chocolate Race](https://cruiseofdimensionality.home.blog/2019/04/21/the-great-chocolate-race/)



### Leave a comment [Cancel reply](/2019/07/24/pc-video-games-we-still-play/#respond)





Δ

 
This site uses Akismet to reduce spam. [Learn how your comment data is processed](https://akismet.com/privacy/).









[Blog at WordPress.com.](https://wordpress.com/?ref=footer_blog)













 



* [Comment](https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/#respond)
* Reblog
* Subscribe
Subscribed




	+ [The Cruise of Dimensionality](https://cruiseofdimensionality.home.blog)







 

 Sign me up 


* Already have a WordPress.com account? [Log in now.](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Fr-login.wordpress.com%2Fremote-login.php%3Faction%3Dlink%26back%3Dhttps%253A%252F%252Fcruiseofdimensionality.home.blog%252F2019%252F07%252F24%252Fpc-video-games-we-still-play%252F)
* [Privacy](#)
* + [The Cruise of Dimensionality](https://cruiseofdimensionality.home.blog)
	+ [Customize](https://cruiseofdimensionalityhome.wordpress.com/wp-admin/customize.php?url=https%3A%2F%2Fcruiseofdimensionalityhome.wordpress.com%2F2019%2F07%2F24%2Fpc-video-games-we-still-play%2F)
	+ Subscribe
	Subscribed
	+ [Sign up](https://wordpress.com/start/)
	+ [Log in](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Fr-login.wordpress.com%2Fremote-login.php%3Faction%3Dlink%26back%3Dhttps%253A%252F%252Fcruiseofdimensionality.home.blog%252F2019%252F07%252F24%252Fpc-video-games-we-still-play%252F)
	+ [Copy shortlink](https://wp.me/paB9Fy-1A)
	+ [Report this content](https://wordpress.com/abuse/?report_url=https://cruiseofdimensionality.home.blog/2019/07/24/pc-video-games-we-still-play/)
	+ [View post in Reader](https://wordpress.com/read/blogs/156618668/posts/98)
	+ [Manage subscriptions](https://subscribe.wordpress.com/)
	+ Collapse this bar






 





























































Loading Comments...



 


Write a Comment...




Email (Required)



Name (Required)



Website











### 
























 


%d 



 

Design a site like this with WordPress.com[Get started](https://wordpress.com/start/?ref=marketing_bar) 





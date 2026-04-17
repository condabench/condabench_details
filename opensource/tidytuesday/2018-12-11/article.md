







How Data Made Me A Believer In New York City’s Restaurant Grades \| FiveThirtyEight

























































































[Skip to main content](#content)



[FiveThirtyEight](/)
--------------------



Search



Search


[ABC News](https://abcnews.go.com/ "ABC News")
Menu




 How Data Made Me A Believer In New York City’s Restaurant Grades 
[Share on Facebook](https://fivethirtyeight.com/features/how-data-made-me-a-believer-in-new-york-citys-restaurant-grades/?share=facebook)
[Share on Twitter](https://fivethirtyeight.com/features/how-data-made-me-a-believer-in-new-york-citys-restaurant-grades/?share=twitter)



* [Politics](https://fivethirtyeight.com/politics/)
* [Sports](https://fivethirtyeight.com/sports/)
* [Science](https://fivethirtyeight.com/science/)
* [Podcasts](https://fivethirtyeight.com/podcasts/)
* [Video](https://fivethirtyeight.com/videos/)
* [Interactives](https://projects.fivethirtyeight.com/)
* [ABC News](https://abcnews.go.com/)








[This is an archived site and is no longer being updated. New 538 articles can be found at www.abcnews.com/538\.](http://abcnews.com/538)








Sep. 2, 2014,
 at
 12:00 PM




How Data Made Me A Believer In New York City’s Restaurant Grades
================================================================





By [Kaiser Fung](https://fivethirtyeight.com/contributors/kaiser-fung/)




 








 





 The Dominique Ansel Bakery, maker of the cronut, was temporarily closed in April by the New York City Health Department. Noam Galai / Getty Images








 The Dominique Ansel Bakery, maker of the cronut, was temporarily closed in April by the New York City Health Department. Noam Galai / Getty Images







One morning in April, the neighbors of Dominique Ansel Bakery, whose owner invented the “cronut” (the pastry famed for combining the croissant and donut), were amused. For the first time in a long time, the tourists who commonly mobbed the little Manhattan bakery had disappeared. Were we finally hearing the popping of the cronut bubble?


Not quite.


A makeshift sign on the door disclosed that the bakery was temporarily closed for failing an inspection by New York City’s health department, which made waves during Mayor Michael Bloomberg’s tenure for initiating a letter grading system for restaurants. The April inspection, Dominique Ansel’s second in seven months, was triggered by an act of citizen journalism. The day before, the Gothamist blog had [published](http://gothamist.com/2014/04/03/cronut_mouse_video.php) a video shot by a customer of a small mouse scurrying inside the store.


In response, the bakery sent a note to its cronut\-deprived fans: “Due to the video that was released showing a small mouse running across the screen for five seconds, the health department used it as evidence to ask us to re\-cement and closed down the bakery for extermination. As a small one\-shop bakery, we often feel like we’re being looked at under a tremendous microscope.”


Did one tiny mouse really close the trendy bakery? I used data from the health department to investigate this question, and the short answer is no. I ran an algorithm to analyze historical data, deducing the relative importance of different factors, including vermin, on restaurant health grades. While certain chefs have complained about specific health inspection rules, after examining the data, I accept the logic behind the grades, and feel pretty confident referencing them now.


Here’s how [New York City’s restaurant grading system](http://www.nyc.gov/html/doh/downloads/pdf/rii/blue-book.pdf) works. There are 68 possible violations, ranging from “Evidence of rats or live rats present in facility’s food and/or non\-food areas” to “Tobacco use, eating or drinking from open container in food preparation, food storage or dishwashing area.” Restaurants rack up points for violations — and receive an A if they have fewer than 14 points, a B if they have between 14 and 27 points and a C for 28 points or more. Each violation can carry a range of points depending on its severity. Only four of the 68 violations relate to physical evidence of vermin — rats, mice, roaches and flies.


As it turns out, to my unpleasant surprise, a restaurant can earn an A while harboring mice or roaches, provided that it has few or no violations of other types. Records show that last fall health inspectors went to a Brooklyn café where they found droppings from mice, rats, roaches and flies. The restaurant amassed 11 points — good enough for an A! Since June 2011, two other restaurants have managed to pull off this act of escape.


Having one type of vermin could be bad luck; having all four looks like total carelessness to me. Recent social\-media commotion around the mouse at Dominique Ansel, roaches at [Blue Ribbon Sushi](http://observer.com/2014/04/signs-of-life-pest-problems-plague-sohos-chicest-food-spots/), and a rat rattling a pastry case at [Dunkin Donuts](http://gothamist.com/2014/04/02/dunkin_donuts_rat_reax.php) indicate that many diners feel the same way. According to [Food Safety Magazine](http://www.foodsafetymagazine.com/magazine-archive1/augustseptember-2012/sanitation-pests-everyday-threats-to-the-human-food-supply/), mice and rats urinate and defecate frequently, spreading diseases such as hantavirus and salmonellosis; flies carry more than 100 kinds of disease\-causing germs; and cockroaches transfer bacteria, parasitic worms and human pathogens.


Using the health department’s data, I created a vermin\-only grading scale, and compared it to the official A\-B\-C restaurant ratings.1 The vermin grades are 0, 1, 2 or 3, corresponding to the number of types of vermin found during an inspection.


![fung-feature-health-grades-1](opensource/tidytuesday/2018-12-11/images/0.png)


As you can see, my vermin grade and the city’s health grades are strongly correlated. Nonetheless, about 24 percent of inspections uncovering two vermin\-related violations resulted in the restaurants receiving As. Among restaurants with one such violation, 40 percent got As. So, contrary to what Dominique Ansel believes, one mouse is unlikely to ruin an inspection.


So if vermin only explain some of a restaurant’s grade, what factors account for the rest?


The most recent restaurant grades [data set](https://nycopendata.socrata.com/Health/Restaurant-Inspection-Results/4vkw-7nck) contains all inspections from Aug. 2, 2010, to July 15, 2014, including the name of the restaurant, the neighborhood, the cuisine,2 the violations, the point score and the grade. I removed data before June 1, 2011, since the low frequency of visits suggests that some grades were not recorded. I also excluded inspections after May 2014, because some 20 percent to 30 percent of those have yet to be resolved. (Restaurants have the option to engage in a lengthy re\-inspection and arbitration process if they receive a grade of B or C.3) Ungraded inspections were also dropped. In total, my database comprises just under 63,000 inspections of about 17,300 New York City restaurants.


The health department’s 68 violation types spread the information too thinly, so I aggregated them to seven key violation groups: vermin, temperature, facilities, food handling, hygiene, contamination and regulatory. An example of a temperature\-related violation is “Hot food item not held at or above 140 F”; an example of a facilities\-related violation is “Sewage disposal system improper or unapproved”; and a food handling violation might be “Raw food not properly washed prior to serving.” A few violations belong to multiple groups — for example, “‘Wash hands’ sign not posted at hand\-washing facility” concerns facilities as well as regulation.


I wanted to explore how different factors — such as violation groups, cuisine groups, year and month of inspection, and neighborhood — contribute to the A\-B\-C grading system.4 The below chart lists the variables sorted by their influence on the grade.


![fung-feature-health-grades-2](opensource/tidytuesday/2018-12-11/images/1.png)


Vermin\-related violations have the biggest influence on restaurant grades. The next most harmful violation group is temperature\-related offenses, which rates only slightly below vermin. Violations related to food handling are also influential, while relatively minor infractions include those grouped under facilities, contamination, regulatory and hygiene.


I used the date of inspection to control for season. According to my model, the month of inspection contributes almost nothing to explaining grades, although the year does have a moderate effect. The type of cuisine and the location of the restaurant (i.e. neighborhood) also don’t appear to predict health inspection failure.5


A more detailed analysis reveals that restaurants started getting better grades in the second half of 2013\. In 2012, the second year of A\-B\-C grading, about 70 percent of restaurants in my database earned As; by the first quarter of 2014, this proportion exceeded 80 percent. The same trend is evident in all five boroughs.


![fung-feature-health-grades-3](opensource/tidytuesday/2018-12-11/images/2.png)


I now believe the system in New York City makes sense. The health grade incorporates a variety of metrics, with reasonable weights. These weights are not explicitly specified in a formula, and they reflect the average behavior of all inspectors, but it is possible to use a statistical model to deduce their values, as I have here. My one complaint: If I were heading the New York City health department, I would shift more consideration to the rats, mice, roaches and flies.







Footnotes
---------



1. Not every restaurant receives one of these letter grades; inspectors can give other scores, primarily P or Z, or some version of “grade pending.”
2. I focused on the 10 most popular cuisine groups. In order of the number of restaurants, the top 10 cuisine categories are American, Italian (including pizza), Chinese, bakeries (including donuts, bagels/pretzels, pancakes/waffles), Latin, delis (including sandwiches, soups, salads), cafes, Mexican, Japanese and Caribbean.
3. If an initial inspection results in a B or C grade, the restaurant owner can post a “Grade Pending” sign while navigating the re\-inspection and arbitration process. In the health department’s database, about 2 percent of historical grades were missing. The number rose to 20 percent to 30 percent in the final two months for which data is available. Any analysis that simply ignores missing grades is severely biased: In the June and July 2014 data, all of the As are counted while most of the Bs and Cs are suppressed.
4. This was a multivariate classification problem. I applied a classification tree methodology (30 percent of the data was held out for validation). I assume the restaurant’s grade is derived from a weighted average of component scores — with each component representing one of the seven violation groups. These components are deduced from the 68 violation types scored by inspectors. The component weights are allowed to vary according to seasonality, cuisine group and neighborhood. The model produces unequal weights for the seven violation groups even though the health department’s rulebook gives equal standing to each of the 68 violation types. One reason for the discrepancy is that there are different numbers of violations under each violation group. Another reason is more subtle. As any baseball fan knows, the rulebook defines the strike zone, but it is the umpire who calls balls and strikes — and each umpire applies his own interpretation of the definition. The tree model summarizes how the average health inspector implements the rules. He or she may have a tendency to cite some of the violations more often, or to consider certain types of violations more severe.
5. When the restaurant grades database first went online, many bloggers analyzed the variation in ratings by [cuisine](http://www.huffingtonpost.com/2013/06/11/new-york-restaurant-health-grades_n_3392571.html) and by [location](http://www.dnainfo.com/new-york/20110209/manhattan/morningside-heights-has-dirtiest-restaurants-study-finds). By hooking up the data to a visualization tool, some websites, including [The New York Times](http://www.nytimes.com/interactive/dining/new-york-health-department-restaurant-ratings-map.html), automatically generate maps of restaurant grades. However, neither cuisine nor neighborhood has much explanatory power for the grades themselves. The proportion of As ranges from 67 percent to 75 percent by borough, but ranges from 9 percent to 82 percent by number of vermin\-related violations.

 


Kaiser Fung is the founder of Principal Analytics Prep, which runs practical training programs for aspiring data scientists. He is the author of “Numbersense.”  [@junkcharts](https://twitter.com/junkcharts)





### Comments









Filed under


[Public Health (65 posts)](https://fivethirtyeight.com/tag/public-health/)








Interactives
------------





Latest Videos
-------------


* ### [Why Biden Is Losing Support Among Voters Of Color](https://fivethirtyeight.com/videos/why-biden-is-losing-support-among-voters-of-color/?cid=rrfeaturedvideo)




[![]()](https://fivethirtyeight.com/videos/why-biden-is-losing-support-among-voters-of-color/?cid=rrfeaturedvideo)
* ### [Should We Trust Polls Campaigns Leak To The Press?](https://fivethirtyeight.com/videos/should-we-trust-polls-campaigns-leak-to-the-press/?cid=rrfeaturedvideo)




[![]()](https://fivethirtyeight.com/videos/should-we-trust-polls-campaigns-leak-to-the-press/?cid=rrfeaturedvideo)
* ### [How Well Can You Tell The 2024 GOP Candidates Apart?](https://fivethirtyeight.com/videos/how-well-can-you-tell-the-2024-gop-candidates-apart/?cid=rrfeaturedvideo)




[![]()](https://fivethirtyeight.com/videos/how-well-can-you-tell-the-2024-gop-candidates-apart/?cid=rrfeaturedvideo)
* ### [What The GOP Primary Looks Like In The Early States](https://fivethirtyeight.com/videos/what-the-gop-primary-looks-like-in-the-early-states/?cid=rrfeaturedvideo)




[![]()](https://fivethirtyeight.com/videos/what-the-gop-primary-looks-like-in-the-early-states/?cid=rrfeaturedvideo)













 Get more FiveThirtyEight 

* [Store](https://cottonbureau.com/stores/fivethirtyeight#/shop)
* [Twitter](https://twitter.com/fivethirtyeight)
* [Facebook](https://www.facebook.com/fivethirtyeight)
* [Data](https://data.fivethirtyeight.com/)
* [RSS](https://fivethirtyeight.com/features/fear-not-readers-we-have-rss-feeds/)




* 
* [Follow @FiveThirtyEight](https://twitter.com/FiveThirtyEight)




* [About Us](https://fivethirtyeight.com/about-us/)
* [Jobs](https://fivethirtyeight.com/jobs/)
* [Masthead](https://fivethirtyeight.com/masthead/)
* [Pitch FiveThirtyEight](https://fivethirtyeight.com/how-to-pitch-fivethirtyeight/)
* [Advertise With Us](https://disneyadsales.com/our-brands/abc-news/)
* [About Nielsen Measurement](http://priv-policy.imrworldwide.com/priv/browser/us/en/optout.html)




 Powered by [WordPress VIP](https://wpvip.com/?utm_source=vip_powered_wpcom&utm_medium=web&utm_campaign=VIP%20Footer%20Credit&utm_term=fivethirtyeight.com) 

* [Terms of Use](https://disneytermsofuse.com/)
* [Privacy Policy](https://disneyprivacycenter.com/)
* [Do Not Sell or Share My Personal Information](https://privacy.thewaltdisneycompany.com/en/dnssmpi/)
* [Your US State Privacy Rights](https://privacy.thewaltdisneycompany.com/en/current-privacy-policy/your-us-state-privacy-rights/)
* [Children's Online Privacy Policy](https://disneyprivacycenter.com/kids-privacy-policy/english/)
* [Interest\-Based Ads](https://preferences-mgr.truste.com/?type=abcnews&affiliateId=11&cid=clicksource_4380645_footer_interestbasedads)



 © 2024 ABC News Internet Ventures. All rights reserved.
 







Close Additional Information
[Terms of Use](https://disneytermsofuse.com/) and [Privacy Policy](https://disneyprivacycenter.com/) and Safety Information/[Your California Privacy Rights](https://disneyprivacycenter.com/notice-to-california-residents/)/[Children's Online Privacy Policy](https://disneyprivacycenter.com/kids-privacy-policy/english/) are applicable to you. © 2024 ABC News Internet Ventures. All rights reserved. [Interest\-Based Ads](https://preferences-mgr.truste.com/?type=abcnews&affiliateId=11&cid=clicksource_4380645_footer_interestbasedads). [Cookie Policy](https://disneyprivacycenter.com/cookies-policy-translations/cookies-policy/).
 
















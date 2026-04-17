







Should Travelers Avoid Flying Airlines That Have Had Crashes in the Past? \| FiveThirtyEight
























































































[Skip to main content](#content)



[FiveThirtyEight](/)
--------------------



Search



Search


[ABC News](https://abcnews.go.com/ "ABC News")
Menu




 Should Travelers Avoid Flying Airlines That Have Had Crashes in the Past? 
[Share on Facebook](https://fivethirtyeight.com/features/should-travelers-avoid-flying-airlines-that-have-had-crashes-in-the-past/?share=facebook)
[Share on Twitter](https://fivethirtyeight.com/features/should-travelers-avoid-flying-airlines-that-have-had-crashes-in-the-past/?share=twitter)



* [Politics](https://fivethirtyeight.com/politics/)
* [Sports](https://fivethirtyeight.com/sports/)
* [Science](https://fivethirtyeight.com/science/)
* [Podcasts](https://fivethirtyeight.com/podcasts/)
* [Video](https://fivethirtyeight.com/videos/)
* [Interactives](https://projects.fivethirtyeight.com/)
* [ABC News](https://abcnews.go.com/)








[This is an archived site and is no longer being updated. New 538 articles can be found at www.abcnews.com/538\.](http://abcnews.com/538)








Jul. 18, 2014,
 at
 8:20 PM




Should Travelers Avoid Flying Airlines That Have Had Crashes in the Past?
=========================================================================





By [Nate Silver](https://fivethirtyeight.com/contributors/nate-silver/)


Filed under [Airline Safety](https://fivethirtyeight.com/tag/airline-safety/)



Get the data on [GitHub](https://github.com/fivethirtyeight/data/tree/master/airline-safety)
GitHub data at [data/airline\-safety](https://github.com/fivethirtyeight/data/tree/master/airline-safety)





 








 





 A memorial with candles that read ‘MH17’ glows silently as unseen churchgoers pray for the victims of Malaysia Airlines flight MH17 from Amsterdam to Kuala Lumpur, at a church in Kuala Lumpur on Friday. Nicolas Asfouri / AFP / Getty Images








 A memorial with candles that read “MH17” silently glows as unseen churchgoers pray for the victims of Malaysia Airlines flight MH17 from Amsterdam to Kuala Lumpur, at a church in Kuala Lumpur on Friday. Nicolas Asfouri / AFP / Getty Images







The [downing of Malaysia Airlines Flight 17](http://www.nytimes.com/interactive/2014/07/17/world/europe/maps-of-the-crash-of-malaysian-airlines-flight-mh17.html?_r=0) in Ukraine on Thursday, following the disappearance of its Flight 370 in March, is the second mysterious incident involving the airline this year. The incidents don’t appear to be related, but that isn’t preventing people from [insisting that they’ll never fly Malaysia Airlines again](https://twitter.com/search?q=never%20fly%20malaysia&src=typd). Some of them will follow through — academic studies have found that high\-profile crashes can [shift passenger demand away](http://www.finance.pamplin.vt.edu/faculty/vs/pdfs/JLE1998.pdf) from the airlines involved in the disasters.


Is this behavior rational? Should we really be less inclined to fly airlines that have had fatal crashes in the past — even when the crashes don’t appear to be their fault? Or are crashes essentially random events that occur at about the same rate on all airlines over the long run? (The two fatal accidents involving Malaysia Airlines this year were the [first for the carrier since 1995](http://aviation-safety.net/database/operator/airline.php?var=5718).)


We can study this by looking at safety records for major commercial airlines over the past 30 years, as based on the [Aviation Safety Network’s database](http://aviation-safety.net/index.php). The method is relatively simple. I’ll break the 30\-year period down into two halves: first from 1985 to 1999, and then from 2000 to 2014\. Then I’ll look to see whether there was a correlation in crash rates from one half of the data set to the other. If we identify a correlation, that will imply that crash risk is persistent — predictable to some extent based on the airline.


I’ll be making a couple of simplifying assumptions:


* First, I’ll include all crashes regardless of their cause. The airline is clearly more culpable in cases such as the [1977 Tenerife disaster](https://www.youtube.com/watch?v=kjLrZ2SDDaU) than others like Flight 17\. But the causes of many other disasters (such as Malaysia Flight 370\) are controversial or poorly understood — I’m not going to try to assign blame.
* Next, I’ll take crash rates on the basis of the number of [available seat kilometers](http://www.atn.aero/analysis.pl?id=1318) (ASKs), which is defined as the number of seats multiplied by the number of kilometers the airline flies.1 ASK figures are taken as of December, 2012\. This implicitly assumes that the number of ASKs has been constant for each airline since 1985, which is obviously not true — some airlines have grown while others have shrunk — but this is a necessary simplification until we can track down some older data. I do, however, exclude any airlines that were not operational as of Jan. 1, 1985,2 and account for some major mergers (so Northwest’s data is combined into Delta’s, and so forth). I also include data for regional subsidiaries under the flagship carrier — so incidents for American Eagle are grouped with the data for American Airlines, for instance.
* I’ll define crashes in three ways:
	+ First, based on the rate of **incidents** as listed in the database, whether or not they resulted in a fatality.
	+ Next, based on the rate of **fatal accidents**.3
	+ Finally, by the rate of **fatalities** among passengers and crew on the airline.


Here’s the data for 56 airlines that were in the [global top 100](http://www.atn.aero/analysis.pl?id=1318) as of December 2012 and which have operated continuously since Jan. 1, 1985\. Airlines are sorted based on the rate of fatalities per ASK.


![silver-datalab-airlines-safety-table-1](opensource/tidytuesday/2018-08-07/images/0.png)


As you should see, the number of fatalities is not very consistent from the first half of the data set to the next. Avianca, the national airline of Colombia, [had a series of major crashes from 1983 through 1990](http://aviation-safety.net/database/operator/airline.php?var=6409). But it has had almost no problems since then — no fatal accidents since 1990, and no incidents of any kind since 1999\. By contrast, Kenya Airways was [fatality\-free until 2000](http://aviation-safety.net/database/operator/airline.php?var=5885) but has had two major accidents since then and ranks as the worst airline since 2000 based on the number of fatalities per ASK.


One or two other carriers, such as Taiwan’s [China Airlines](http://aviation-safety.net/database/operator/airline.php?var=6932) (not be confused with Beijing’s Air China4), have had problems in both halves of the data set. But these cases are more the exception than the rule. Overall, there is no correlation in the rate of fatalities from one period to the next.


![silver-datalab-airlines-safety-2](opensource/tidytuesday/2018-08-07/images/1.png)


Accidents that produce a massive number of fatalities are rare compared to fatal accidents of any kind, however. And fatal accidents represent only about one\-quarter of all incidents listed in the database. So it may be better to compare airlines on the basis of their number of incidents, whether or not they resulted in a fatality, which has the effect of increasing the sample size. These near\-misses can still produce non\-fatal injuries. They may also provide useful evidence about the overall hazard associated with flying a given airline, in the same way that the [number of smaller earthquakes](https://fivethirtyeight.com/features/eric-cantors-loss-was-like-an-earthquake/) in a region over a period of time can be used to predict the likelihood of a catastrophic one.5


![silver-datalab-airlines-safety-3](opensource/tidytuesday/2018-08-07/images/2.png)


Viewed this way, there is a modest correlation from one period to the next.6 There are also a few major outliers in the chart: two are [Pakistan International Airlines](http://aviation-safety.net/database/operator/airline.php?var=4931) and [Ethiopian Airlines](http://aviation-safety.net/database/operator/airline.php?var=6263), which have had a persistently high rate of incidents. A third outlier, Russia’s Aeroflot, had an [extraordinarily high number of reported incidents in the 1990s](http://aviation-safety.net/database/operator/airline.php?var=6834) — many of them attempted hijackings around the time of the breakup of the Soviet Union — but only an average number in recent years. There is still a positive correlation even if those three airlines are excluded, however, which rates as modestly statistically significant7 — some airlines are slightly safer to fly than others.


Our preliminary answer, then, is that an airline’s track record tells you something about its probability of future crashes — although not a lot, and only if looked at in the right way. In particular, you should look toward an airline’s rate of dangerous incidents of any kind rather than its number of fatalities or fatal accidents. These near\-misses are more consistent from period to period — and could result in a deadly crash the next time around.


But there’s a better rule to follow. If you’re insistent on minimizing your crash risk, you should avoid airlines from developing countries.


Let’s combine our three measures of crash rates — incidents, fatal accidents and fatalities — into a single measure which I’ll call the airline’s safety score. I calculate it as follows:


* For each category, subtract an airline’s crash rate from the average for all airlines since 1985\. This gives safer airlines positive scores and less safe airlines negative scores.
* Multiply the result by the square root of the number of seat kilometers flown. This gives more credit to an airline that has achieved a strong safety record over a larger sample of flights.
* [Standardize](http://en.wikipedia.org/wiki/Standard_score) the score in each category to calculate how many standard deviations an airline is above or below the mean. Then average the scores from the three categories together. This is the safety score.


Positive scores indicate a safe track record — Australia’s Qantas, for instance, which is [famous for avoiding crashes](https://www.youtube.com/watch?v=KeYf-rhMQIQ) — has a safety score of \+0\.71\. By contrast, Pakistan International Airlines has a score of \-1\.49\.


![silver-datalab-airlines-safety-table-4](opensource/tidytuesday/2018-08-07/images/3.png)


The chart also lists the [per\-capita gross domestic product](http://en.wikipedia.org/wiki/List_of_countries_by_past_and_future_GDP_(PPP)_per_capita) for the airline’s home country as of 1999 (the middle of the 30\-year period). The correlation between a country’s wealth and the crash rates of its airlines is quite strong.8 Over the past 30 years, the top 10 safety scores belong to two airlines from the United States (Southwest Airlines and United Airlines), two from the United Kingdom, and one each from Canada, Australia, Hong Kong, Singapore, Germany and the Netherlands. By contrast, the 10 worst scores are for airlines from Colombia, Egypt, Ethiopia, Indonesia, Kenya, Morocco, Pakistan, the Philippines, Russia and Taiwan. In fact, if you want to predict an airline’s future rate of crashes, you’re best off looking at its home country’s GDP and largely ignoring its track record.9


Perhaps this shouldn’t be surprising. Commercial airlines are subject to extremely stringent safety standards, and the same standards are applied to all airlines from the same country or region. Richer countries, in air travel and [many other aspects of public planning](http://www.bath.ac.uk/e-journals/jtep/pdf/Volume_34_Part_2_169-188.pdf), can afford to buy more safety in the form of higher prices and more expensive regulations.


So should you never fly an airline from a developing country again? No, that would be silly — commercial airline travel is an [extraordinarily safe means of transit](https://fivethirtyeight.com/features/skies-are-as-friendly-as-ever-911-al/) overall. What you should do is avoid airlines on blacklists, such as that periodically [put out by the European Union](http://en.wikipedia.org/wiki/List_of_air_carriers_banned_in_the_European_Union). (None of the airlines on the list of 56 above is currently on the EU’s blacklist, although one, Pakistan International Airlines, [has been in the recent past](http://news.bbc.co.uk/2/hi/6418891.stm).) Otherwise — even on Malaysia Airlines — the risk of being involved in a crash is very low, and that risk doesn’t increase much after a recent disaster.


**CORRECTION (July 23, 9:54 a.m.):** The tables in a previous version of this post used an incorrect denominator in calculating incidents, fatal accidents and fatalities. They had been assuming 80 percent rather than 100 percent of seats were filled by passengers, in accordance with standard industry [load factors](http://en.wikipedia.org/wiki/Passenger_load_factor). However, the definition of an available seat kilometer (ASK), the statistic used elsewhere in the article, is based on the number of seats available and not how many of them were filled. The numbers in the tables have been changed to reflect the proper definition of an ASK.


In addition, we double\-checked the numbers for all 56 airlines and found a small number of accidents that had previously been missed, as well as a couple of typos. These have been corrected. These changes do not significantly affect the relative ordering of the airlines or the overall conclusion of the article.


**UPDATE (July 23, 9:54 a.m.):** A number of readers were confused about the numbers described in the tables. They list the number of incidents, fatal accidents and fatalities per one trillion available seat kilometers (ASKs) flown, and not the raw numbers. This is an important distinction: For instance, United Airlines flies about 24 times more miles than Royal Air Maroc. United has had more accidents overall, but it has had considerably fewer per ASK. However, we’ve inserted the following table for people who would prefer to see the unadjusted numbers. We’ve also posted the [data used](https://github.com/fivethirtyeight/data/tree/master/airline-safety) in this article on [GitHub](https://github.com/fivethirtyeight).


![silver-datalab-airlines-safety-table-5](opensource/tidytuesday/2018-08-07/images/4.png)







Footnotes
---------



1. One could argue for a different definition of risk — for instance, based on the number of takeoffs and landings, since [relatively few crashes occur in the cruise phase of flight](http://www.planecrashinfo.com/cause.htm). That data is hard to find for international carriers, however, whereas ASKs are more commonly reported in the industry.
2. I also exclude airlines that principally flew charter flights for all or part of the period.
3. Fatal accidents, by my definition, must result in the death of a member of the passenger or crew — ground fatalities are not included.
4. Air China is not included in the table since it was founded after 1985\. It has a decent [safety record](http://aviation-safety.net/database/operator/airline.php?var=6695).
5. The potential downside is that it’s harder to define a dangerous incident than a fatal accident, so there may be inconsistent reporting standards in the data set.
6. The correlation coefficient is .37
7. At the 95 percent confidence level.
8. The correlation between the natural logarithm of per\-capita GDP in 1999 and an airline’s safety score over 1985\-2014 is .70\.
9. For instance, if you conduct a regression on an airline’s safety score from 2000\-2014 on the basis of its safety score from 1985\-1999 and the natural logarithm of its GDP in 1999, the GDP variable is highly statistically significant while its past safety score provides no additional predictive power.

 


Nate Silver founded and was the editor in chief of FiveThirtyEight.   [@natesilver538](https://twitter.com/natesilver538)





### Comments









Filed under


[Ukraine (68 posts)](https://fivethirtyeight.com/tag/ukraine/)
[Airline Safety (5\)](https://fivethirtyeight.com/tag/airline-safety/)
[Malaysia Airlines Flight 370 (5\)](https://fivethirtyeight.com/tag/malaysia-airlines-flight-370/)
[Plane Crashes (4\)](https://fivethirtyeight.com/tag/plane-crashes/)








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
 
















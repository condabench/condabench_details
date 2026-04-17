




Visualizing the Geography of FM Radio – Data Stuff









































































[Data Stuff](https://erdavis.com/)
==================================


It's stuff I made with data!
----------------------------




Menu
[Skip to content](#content)
* [Home](https://erdaviscom.wordpress.com)
* [Datasets](https://erdavis.com/datasets/)
* [Prints](https://erdavis.com/prints/)
* [About](https://erdavis.com/about/)
* [Contact Me](https://erdavis.com/contact/)







[January 4, 2020January 24, 2020](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/) [erinrdavis](https://erdavis.com/author/erinrdavis/)
Visualizing the Geography of FM Radio
=====================================



This project, like [the one before it](https://erdavis.com/2019/12/25/whats-the-biggest-one-hit-wonder-on-spotify/), started as an offshoot of another project that I’ll finish… someday…


I start one project, which brings up questions I need to answer in other projects, so I start those projects, which lead to more questions… and before I know it I have a tangled mess that’ll take months to sort out.  To illustrate, there’s currently 11 projects in my “Active” queue and 11 more in my “Paused” queue. I’m personally very proud that I get anything done at all!


For this particular tangled project mess, I needed to see how many classical music radio stations there are in the States. That quickly lead to wanting to plot where those classical stations broadcast. *That* lead to a burning desire to map all radio station broadcast areas, *ever,* and also to map how many radio stations broadcast in a given area.


Getting the Data
----------------


Amazingly, I was able to satisfy these admittedly strange desires fairly easily.


The FCC [provides service contours](https://www.fcc.gov/media/radio/fm-service-contour-data-points) for more than 20,000 FM radio stations. A service contour is the area in which the radio station may be received without interference from other stations broadcasting on the same frequency. Radio stations can usually be received at much further distances than the service contours indicate, but the FCC doesn’t provide data on the limits of station reception.


I took these service contours and joined them to a [list of licensed stations](https://www.fcc.gov/media/radio/fm-query) to hopefully filter out defunct or otherwise irrelevant stations. To be honest, I’m not sure I totally understand the results on this list, as there do seem to be duplicate stations with the same service contours. In the absence of any more information or guidance, I took the data on good faith and used it as it came.


**(Edit:** I now know I incorrectly included station construction permits in my data. Hopefully some day I’ll get around to correcting my maps, but till then, be aware they aren’t 100% correct.)


Finally, I was able to identify the broadcasting formats (e.g. Top 40, Adult Contemporary) for about half the stations on my list thanks to [radio\-locator.com](https://radio-locator.com/).


Mapping FM Radio service contours
---------------------------------


I started by simply plotting the service contours of the 20,000\-odd stations on my list. I love the way this looks, like phosphorescent jellyfish or raindrops on water.


[![radio_circles_final](opensource/tidytuesday/2022-11-08/images/0.png)](https://erdavis.com/wp-content/uploads/2020/01/radio_circles_final.png)


I also mapped the service contours of stations with particular formats:


![Final_genre](opensource/tidytuesday/2022-11-08/images/1.png)


Next, I calculated the number of stations available at any given point:


[![Radio_Fill_Final](opensource/tidytuesday/2022-11-08/images/2.png)](https://erdavis.com/wp-content/uploads/2020/01/radio_fill_final.png)


Unexpectedly, at least to me, the Salt Lake City area beats the rest of the country by a long shot. Some areas of SLC can receive over 60 stations without interference from other stations on the same channel! By comparison, the SF Bay Area is a distant second with 50\-odd stations available.


I’m honestly not sure if this is a flaw in the data or the reality on the ground. A manual review didn’t turn up any suspiciously duplicated information or anything else that looked off. Anyone know of any reason why the state might be so radio\-obsessed?


I loved this map because it looks like drops of ink spreading in water. The effect is more pronounced when looking at individual states or cities:


[![radio_AZ_45](opensource/tidytuesday/2022-11-08/images/3.png)](https://erdavis.com/wp-content/uploads/2020/01/radio_az_45.png)


[![radio_OH_38](opensource/tidytuesday/2022-11-08/images/4.png)](https://erdavis.com/wp-content/uploads/2020/01/radio_oh_38.png)


TV Stations
-----------


The FCC provides the same service contour data for broadcast TV, so of course I had to make maps for that as well.


[![tv_circles_final](opensource/tidytuesday/2022-11-08/images/5.png)](https://erdavis.com/wp-content/uploads/2020/01/tv_circles_final.png)


I would love to know what those horizontal chains of TV stations in the Midwest are! Google has completely failed me in finding out.


**(Edit:** Several folks contacted me to explain these are repeaters serving small communities along the interstates. They don’t have enough population to justify stations of their own, so they get their broadcasts from a nearby large city.)


[![tv_Fill_Final](opensource/tidytuesday/2022-11-08/images/6.png)](https://erdavis.com/wp-content/uploads/2020/01/tv_fill_final.png)


Again, Utah sticks out. There’s tons of tiny TV stations scattered across the state in a way I don’t see anywhere else. It also appears the area around Cedar City receives more than 100 stations–more than SoCal or NYC! As with the radio stations, I don’t know if this is an issue with the data or the reality on the ground. I’d really like to find out what exactly is going on, as it’s unlike anything else in the country.


The “ink in water” appearance is even more pronounced on these than the radio station one, in my opinion.


[![tv_GA_72](opensource/tidytuesday/2022-11-08/images/7.png)](https://erdavis.com/wp-content/uploads/2020/01/tv_ga_72.png)


[![tv_MN_40](opensource/tidytuesday/2022-11-08/images/8.png)](https://erdavis.com/wp-content/uploads/2020/01/tv_mn_40.png)


In conclusion
-------------


This was a lovely exercise in mapping a bit differently than what I’ve seen out there. I took this in a more artistic than informational direction (admittedly the lack of AK and HI on the maps was due to my aesthetic preferences), but I do think there’s insights to be had from the maps.


One insight that has eluded me, though, is why Utah is so darn strange when it comes to broadcasting. It has many more radio and TV stations than other states, and they’re distributed weirdly, too. Maybe a Utahan could opine?


### Share this:

* [Twitter](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?share=twitter "Click to share on Twitter")
* [Facebook](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?share=facebook "Click to share on Facebook")
* 
Like Loading...

### *Related*


 

* [maps](https://erdavis.com/category/maps/)
* [r](https://erdavis.com/category/r/)
* [Uncategorized](https://erdavis.com/category/uncategorized/)
 

 

Published by erinrdavis
-----------------------




[View all posts by erinrdavis](https://erdavis.com/author/erinrdavis/) 





Post navigation
---------------


[Previous What’s the biggest one hit wonder on Spotify?](https://erdavis.com/2019/12/25/whats-the-biggest-one-hit-wonder-on-spotify/)[Next Shipwrecks of the Arctic](https://erdavis.com/2020/02/24/shipwrecks-of-the-arctic/)
 


68 comments
-----------


1. **Donal** says: 

[January 6, 2020 at 1:59 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-516) 


Really enjoyable post and the graphics are amazing, fair play to you!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=516&_wpnonce=1c3c3a2bf8)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=516#respond)
3. **Colleen Zimmerman** says: 

[January 7, 2020 at 10:00 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-525) 


As usual, I find these maps fascinating! Beautiful and there’s always a bit of surprising information. I thought POP was King, but based on the genre’s displayed, it looks like Country and Religious are King. Since you didn’t include the Top 40 genre, I assume it wasn’t as interesting. I wish I knew someone in broadcasting….I want to print these out, have them framed and give them away as a gift!!! Some of them look like you had fun playing around with a watercolor brush!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=525&_wpnonce=6167a7155d)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=525#respond)
5. **Ashley Howard** says: 

[January 15, 2020 at 1:54 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-558) 


Your maps are really interesting. My theory on the radio stretches in the midwest is that they are highway info stations along the major freeways. Regarding Utah, did you read this article? <https://www.uen.org/utah_history_encyclopedia/b/BROADCAST_HISTORY.shtml> “IN the 1980s, the Salt Lake market became attractive to investors and to large corporations, which brought in corporate management and programming teams and infused cash into the market. As a result, the Salt Lake market became among the most competitive in the country, with more than forty radio stations.”


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=558&_wpnonce=765c15c5cd)Liked by [1 person](#)



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=558#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 22, 2020 at 5:50 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-575) 
	
	
	You could be on to something–they do follow major east\-west highways. They were in the TV station data, but I wonder if that might be a mistake?
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=575&_wpnonce=1f0c679396)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=575#respond) 
		+ **[Scott](http://gravatar.com/lawsonst)** says: 
		
		[January 24, 2020 at 8:40 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-597) 
		
		
		Some of it could be Highway info radio stations, but you also have to remember that it’s REALLY sparsely populated out on the plains. Once you get west of I\-29 (North\-South interstate through KC, Omaha, Sioux Falls, Fargo), there’s not many towns big enough to support much media. Those that are big enough are usually located right along the major interstates.
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=597&_wpnonce=2cb4a5d2c4)Like
		+ **Will P.** says: 
		
		[January 24, 2020 at 3:37 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-604) 
		
		
		Could it also be older traces than the highways themselves: highways following major transcontinental rail lines that came before them (and overland trails before them), which led to more and larger settlements along those lines than just north or south of them, which are then more likely to have TV and/or radio stations.
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=604&_wpnonce=b5caa3ef55)Like
		+ **Raymie Humbert** says: 
		
		[August 14, 2020 at 12:49 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-951) 
		
		
		There are a lot of LPTV construction permits held for spectrum, for whatever reason. For instance, in Sheffield TX on I\-10, the only “receivable” stations belong to two companies: CTB SPECTRUM SERVICES TWO, LLC and SPECTRUM EVOLUTION, INC.
		
		
		They are just pure spectrum plays, not even TV repeaters.
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=951&_wpnonce=3a95eb6c4d)Like
	* **[William Goldsmith](https://radioparadise.com)** says: 
	
	[January 24, 2020 at 9:15 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-598) 
	
	
	Probably the most important factor when it comes to Utah is that SLC is a long way from any other significant population centers. That means that more channels are available — channels that would be taken in cities 100\-200 miles away, if there were any. The topography of the area (largely flat, surrounded by mountains) is also a factor.
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=598&_wpnonce=26f4828058)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=598#respond)
7. **Erika McVey** says: 

[January 22, 2020 at 9:43 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-572) 


This is awesome! I think it would actually be a cool thing to sell prints of as well. They look artsy and abstract, but my nerdy self would love knowing those weren’t actually just ink blots or random jelly fish shapes covering a print of my state.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=572&_wpnonce=8f6553aa29)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=572#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 22, 2020 at 5:27 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-574) 
	
	
	Thanks! I could generate a .png for a specific state if you’re interested–less effort than loading prints onto the site, haha
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=574&_wpnonce=67cd04242a)Liked by [2 people](#)
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=574#respond) 
		+ **[Tod Robbins](https://todrobbins.com)** says: 
		
		[January 23, 2020 at 2:38 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-579) 
		
		
		I’ll take a PNG for Utah, please!
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=579&_wpnonce=ea687d0290)Like
		+ **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
		
		[January 23, 2020 at 5:18 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-584) 
		
		
		here you go: <https://imgur.com/a/kBUwLdA>
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=584&_wpnonce=a0f813a3c6)Like
		+ **AndyC** says: 
		
		[January 24, 2020 at 6:50 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-594) 
		
		
		Could I get a PNG for Virginia? Thanks in advance!
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=594&_wpnonce=6ec76a4a91)Like
		+ **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
		
		[January 24, 2020 at 6:26 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-609) 
		
		
		here you go: <https://imgur.com/a/masecSH>
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=609&_wpnonce=0ec66acc7d)Like
		+ **Erika McVey** says: 
		
		[January 24, 2020 at 8:23 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-595) 
		
		
		Could I get one for South Carolina? 🙂 Thank you!
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=595&_wpnonce=d16b0d1dc9)Like
		+ **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
		
		[January 24, 2020 at 6:27 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-610) 
		
		
		Here you go: <https://imgur.com/a/masecSH>
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=610&_wpnonce=cc90ea7187)Like
		+ **Adam** says: 
		
		[January 26, 2020 at 3:26 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-623) 
		
		
		Any chance you’d be willing to create a PNG for Kansas and Illinois? Fantastic work!
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=623&_wpnonce=726fe8b9a3)Like
		+ **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
		
		[January 27, 2020 at 4:58 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-632) 
		
		
		
		
		> [View post on imgur.com](https://imgur.com/a/TvPEyp1)
		
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=632&_wpnonce=9b47406897)Like
9. **[Visualizing the \#Geography of FM Radio – GeoNe.ws](https://geone.ws/visualizing-the-geography-of-fm-radio/)** says: 

[January 23, 2020 at 4:22 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-576) 


\[…] [https://erdavis.com/2020/01/04/visualizing\-the\-geography\-of\-fm\-radio/](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/) \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=576&_wpnonce=d01d511640)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=576#respond)
11. **JG42** says: 

[January 23, 2020 at 10:44 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-577) 


Nitpick: I figured Gospel would have been included in Religious. What was the differentiation here?


Great work!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=577&_wpnonce=f8b632aee7)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=577#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 23, 2020 at 4:41 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-581) 
	
	
	The categories are what radio\-locator.com provided–my guess is that religious radio is more spoken\-word heavy (though that’s just a guess)
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=581&_wpnonce=6c28531682)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=581#respond)
13. **wally bloss** says: 

[January 23, 2020 at 12:45 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-578) 


Having lived in mountainous Utah there are hundreds of translators which relay a specific station. Utah Public Radio covers much of the large state by 75 or more of these tiny devices. They may only cover a small valley – 10 miles max etc. Very different from the “flatlands” where signals propagate further.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=578&_wpnonce=3c1be4f2c5)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=578#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 23, 2020 at 4:42 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-582) 
	
	
	Thanks for the info! Any idea why it’s mostly a Utah thing and not also in other mountainous states?
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=582&_wpnonce=ba0a08e56c)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=582#respond)
15. **glen** says: 

[January 23, 2020 at 3:19 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-580) 


the tv situation in Utah is due to the translators. they have to have small tv stations behind the mountain so that those folks can get a signal.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=580&_wpnonce=f916e84366)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=580#respond)
17. **[John Stewart](http://johnastewart.org)** says: 

[January 23, 2020 at 7:23 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-586) 


I’d be really interested in the maps for talk radio stations, especially if you knew the political leanings. I doubt that your data set has that information and they might be more prevalent on AM anyway.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=586&_wpnonce=931bac6d24)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=586#respond)
19. **John Mark** says: 

[January 23, 2020 at 10:51 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-587) 


I would love an FM map of WA and ID!  

Cool project!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=587&_wpnonce=16245050d7)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=587#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 24, 2020 at 6:26 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-608) 
	
	
	here you go: <https://imgur.com/a/masecSH>
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=608&_wpnonce=075f0f7a22)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=608#respond)
21. **[College Radio Watch: Mapping U.S. Radio and More News \- Radio Survivor](http://www.radiosurvivor.com/2020/01/24/college-radio-watch-mapping-u-s-radio-and-more-news/)** says: 

[January 24, 2020 at 5:12 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-590) 


\[…] crafted by Erin Davis. While it’s not a pragmatic guide to find radio stations, her beautiful service contour maps give a general sense of how certain formats of FM radio are dispersed across the continental United \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=590&_wpnonce=ba6ebd6aa2)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=590#respond)
23. **[BJ Mora](http://www.graceradio.net)** says: 

[January 24, 2020 at 5:48 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-591) 


Thank you for this! The reason that licensed stations may have more than one listing with similar contours if if they made an application for any kind of (minor) change – whether technical or administrative. If there were a way to filter out CPs (construction permits), that also might help.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=591&_wpnonce=4f0c365fb5)Liked by [1 person](#)



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=591#respond)
25. **[beej6](http://bjmora.wordpress.com)** says: 

[January 24, 2020 at 5:52 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-592) 


You may see stations with more than one (similar) listing if they have a construction permit (CP) pending or approved, or if they have a pending application for any other kind of minor change, whether technical or administrative. If you could filter our CPs at least, that might clear up some data.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=592&_wpnonce=405f323daf)Liked by [1 person](#)



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=592#respond)
27. **[\=\=\= popurls.com \=\=\= popular today](http://popurls.com/pop/)** says: 

[January 24, 2020 at 6:01 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-593) 


\[…] Visualizing The Geography Of FM Radio \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=593&_wpnonce=5254c22b9b)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=593#respond)
29. **ellan** says: 

[January 24, 2020 at 8:28 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-596) 


Could the horizontal chains have something to do with the Long Lines network?  

[https://99percentinvisible.org/article/vintage\-skynet\-atts\-abandoned\-long\-lines\-microwave\-tower\-network/](https://99percentinvisible.org/article/vintage-skynet-atts-abandoned-long-lines-microwave-tower-network/)


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=596&_wpnonce=1d53d1364d)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=596#respond)
31. **Mildred Bonk** says: 

[January 24, 2020 at 10:20 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-599) 


Do the horizontal chains of stations in the midwest match up with an interstate or some other large highway?


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=599&_wpnonce=454a47f4f2)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=599#respond)
33. **Drew** says: 

[January 24, 2020 at 11:42 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-600) 


The horizontal chains are likely the interstates.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=600&_wpnonce=70fd1f3a20)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=600#respond)
35. **[Warren Chase](https://digitaleye.com)** says: 

[January 24, 2020 at 12:51 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-601) 


You’ve created tons of great graphic designs outta already interesting data. Keep up the good work. If it’s easy enough to pull little ole Delaware outta the mix, I wouldn’t mind a PNG, or if easier the mid\-east coast. Don’t feel obligated though!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=601&_wpnonce=34152564fb)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=601#respond) 
	* **[Warren Chase](https://digitaleye.com)** says: 
	
	[January 24, 2020 at 1:25 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-602) 
	
	
	BTW, the “horizontal chains” you see look like they correspond with major roadways running west out of Minneapolis, Sioux Falls, Kansas City, and San Antonio. I may be wrong on that though.
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=602&_wpnonce=c73bc1e1d4)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=602#respond)
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 24, 2020 at 6:27 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-611) 
	
	
	here you go: <https://imgur.com/a/masecSH>
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=611&_wpnonce=a771ce30f4)Liked by [1 person](#)
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=611#respond)
37. **[Warren Chase](https://digitaleye.com)** says: 

[January 24, 2020 at 1:27 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-603) 


BTW, the “horizontal chains” you see look like they correspond with major roadways running west out of Minneapolis, Sioux Falls, Kansas City, and San Antonio. I may be wrong on that though.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=603&_wpnonce=c330bea735)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=603#respond)
39. **Fred Baker** says: 

[January 24, 2020 at 4:36 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-605) 


I am very familiar with the FCC Query FM site. Many FM stations have auxiliary facilities, which are not on when the main station operates. These show with an AUX on the top line to the right. They should not be in your data.


Further, you will also see Construction Permits. These are noted with a CP in the same position as above. These stations are generally not on the air. The stations that show with a LIC are licensed and generally on\-the\-air. 


The strings of smaller FMs are FM translators (FX), which repeat other stations, and low power non\-commercial community stations (LP). These are actually on air.


TV also has translators, which rebroadcast other stations in larger cities. You will see translators mostly along a road or interstate, making them look like they are in a line. 


I hope this helps you refine your map, which is actually already very informative. Thanks for all your work!


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=605&_wpnonce=05884b80f7)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=605#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 24, 2020 at 6:02 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-606) 
	
	
	Thank you so much for this super informative comment! I found that my data didn’t have any AUX items, but there were plenty of construction permits cluttering it up. Now to get the energy to reprise the project 😛
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=606&_wpnonce=c811fc1065)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=606#respond)
41. **Michelle Bradley** says: 

[January 24, 2020 at 6:18 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-607) 


Nice maps. One of my favorite sayings is “contours can be very deceiving”. A service contour is based on the height above average terrain in 360 different directions based on the elevations between 2 and 10 miles from the antenna site. Some contours, especially in mountainous areas will extend into areas that are blocked by mountain ranges more than 10 miles away. In some of those areas, FM boosters are used.


Other commenters are right about the fact that construction permits, auxiliary facilities, as well as deleted licenses come in to this. You must also keep in mind that there are problems with the FCC data right now because of the conversion of FM from the old CDBS system to the new LMS system. Some recently modified stations are showing active in CDBS on facilities that are not operating anymore (because they were changed in LMS). As one of the largest aggregators of FCC broadcast data (much much larger than radio\-locator), I deal with these issues on a daily basis. The current issues with the CDBS/LMS conversion may be driving some of those numbers higher… but these maps are a good high level observation. 


For much more information and fun with broadcast data, visit <https://fccdata.org> and <https://recnet.com> .. when you look at station records, you can see the multiple records that others are talking about. 


The only true way to get coverage is to use a terrain\-based propagation model like Longley\-Rice. 


Again, great job on the maps!


Michelle Bradley  

Founder  

REC Networks  

<https://recnet.com>


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=607&_wpnonce=6d0abcfac9)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=607#respond)
43. **Fred Baker** says: 

[January 24, 2020 at 7:23 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-612) 


To answer your question about Salt Lake City, it is in the middle of nowhere, as far as radio signals go. Therefore, virtually all frequencies were available backbwhen they started building FMs. Normally, you have to have .8 mHz between two higher power stations. If there is a station on 99\.1, there can’t be another co\-located station till 99\.9\. However, with the mountainous terrain down one side of the populated area, and by showing that an interfering contour does not reach the ground, or to where people can go, it is possible to fit another lower power station between those. Then, do the same a few miles away, and you can fill up the entire band. Because FM is line of sight, and they have mountain tower sites, lower power FM stations can serve a large area of population. In this instance, you can literally fill almost the entire FM band. There are 101 FM frequencies in the US. The same thing for San Francisco. One side is the Pacific Ocean. Mountains limit signals from the east, and those, and the coast range mountains, allow lower power stations as above. 


On another subject, the contours you are using are FCC predicted contours based on a method originally devised in the 1950s. They underestimate coverage. The outer contour the Commission uses is the predicted 60 dBu or 1 millivolt per meter contour. I’d add at least 15% to those, but if you can get them, Rice\-Longley maps are quite accurate. They are generated by massive terrain data and RF data crunching. They are used by most savvy consultants, engineers, and management for all real world FM (and cellular) coverage decisions. However, I do not know of a national database that is freely available. 


 I hope that helps explain things, and again, thanks for a fascinating representation of overall coverage.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=612&_wpnonce=32b3e133e4)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=612#respond)
45. **David Nash** says: 

[January 24, 2020 at 11:52 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-613) 


Nice maps. I would be interested in seeing a map for North Carolina. Thank you.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=613&_wpnonce=c0fb5c86cd)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=613#respond)
47. **[Henry Loeser](http://www.radioexpert.org)** says: 

[January 25, 2020 at 2:05 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-614) 


I’d be keen to see a LPFM map 🙂


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=614&_wpnonce=8105df9bca)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=614#respond)
49. **[Hoe Amerika sy energie gebruik, gevisualiseer \- Go Solar Now](https://gosolarnow.co.za/hoe-amerika-sy-energie-gebruik-gevisualiseer/)** says: 

[January 25, 2020 at 3:30 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-615) 


\[…] Visualisering van die geografie van FM\-radio \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=615&_wpnonce=dfa40331a8)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=615#respond)
51. **[نیکول کیدمن در حال مخفی شدن است … چیزی در تریلر بی نظیر برای HBO's “Undoing” – Europe Dating Online](https://www.grendelproject.nl/%d9%86%db%8c%da%a9%d9%88%d9%84-%da%a9%db%8c%d8%af%d9%85%d9%86-%d8%af%d8%b1-%d8%ad%d8%a7%d9%84-%d9%85%d8%ae%d9%81%db%8c-%d8%b4%d8%af%d9%86-%d8%a7%d8%b3%d8%aa-%da%86%db%8c%)** says: 

[January 25, 2020 at 4:53 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-616) 


\[…] Visualizing The Geography Of FM Radio \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=616&_wpnonce=b9d7d0b63e)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=616#respond)
53. **[How Effective Are Masks In Protecting You From The Coronavirus? – Europe Dating Online](https://www.plein66.nl/how-effective-are-masks-in-protecting-you-from-the-coronavirus/)** says: 

[January 26, 2020 at 12:50 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-618) 


\[…] Visualizing The Geography Of FM Radio \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=618&_wpnonce=4342514c77)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=618#respond)
55. **[What’s The Best Way To Survive A Plane Crash? – Europe Dating Online](http://www.lacne.be/whats-the-best-way-to-survive-a-plane-crash/)** says: 

[January 26, 2020 at 3:54 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-619) 


\[…] Visualizing The Geography Of FM Radio \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=619&_wpnonce=6429e2ea1c)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=619#respond)
57. **[Tha Dood](https://vk.com/realfreeradio)** says: 

[January 26, 2020 at 12:28 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-622) 


Hmmmmmmmmm…. Looks like an artist’s interpretation of the older, late, Bruce Elving: FM Atlas maps.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=622&_wpnonce=2012cdedf8)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=622#respond)
59. **Michael W Scheel** says: 

[January 26, 2020 at 5:38 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-625) 


A great way to visualize information. If you look at nighttime photos of the United States and pay attention to states like Iowa. You will see lines of towns that were built along side the railroads. West of the first line of states of the Mississippi River you can see some arranged on sides of either railroads or trails.  

I would like get both Iowa and Illinois if possible.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=625&_wpnonce=4e15e358cc)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=625#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 27, 2020 at 4:58 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-633) 
	
	
	
	
	> [View post on imgur.com](https://imgur.com/a/TvPEyp1)
	
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=633&_wpnonce=d868b7520d)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=633#respond)
61. **John** says: 

[January 26, 2020 at 10:22 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-629) 


I’d like California maps for AM and FM and TV broadcast stations, please. Thank you.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=629&_wpnonce=0341850737)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=629#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 27, 2020 at 4:58 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-634) 
	
	
	
	
	> [View post on imgur.com](https://imgur.com/a/TvPEyp1)
	
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=634&_wpnonce=36d022b112)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=634#respond)
63. **[2020 weeknote 3 – Paul Capewell](http://paulcapewell.com/2020/01/23/2020-weeknote-3/)** says: 

[January 27, 2020 at 8:48 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-630) 


\[…] I’m on the subject of radio, I saw this great visualisation of American FM stations from Erin Davis (via Robin Sloan) recently, which I \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=630&_wpnonce=6278eb00ef)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=630#respond)
65. **Jerome** says: 

[January 27, 2020 at 9:34 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-631) 


These maps are incredible! Were you ever able to plot where classical radio stations broadcast?


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=631&_wpnonce=21aeed100a)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=631#respond) 
	* **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
	
	[January 27, 2020 at 4:59 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-635) 
	
	
	Thanks! Good catch–I kept that plot back to post with that project (analyzing the current popularity of classical music) when I’m done
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=635&_wpnonce=5b3ca13d0c)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=635#respond) 
		+ **[nytcomments](http://nytcomments.wordpress.com)** says: 
		
		[January 27, 2020 at 5:14 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-636) 
		
		
		Awesome, looking forward to it!
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=636&_wpnonce=b1413dc9e5)Like
	* **[Tom Thomas](http://classicalmusicrising.org)** says: 
	
	[January 29, 2020 at 12:51 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-640) 
	
	
	It would be great if we could eventually publish your classical station map at classicalmusicrising.org
	
	
	[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=640&_wpnonce=738c062a47)Like
	
	
	
	[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=640#respond) 
		+ **[erinrdavis](https://erdaviscom.wordpress.com)** says: 
		
		[January 29, 2020 at 6:17 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-643) 
		
		
		Sure! I actually have some questions for you–I’ve been looking for data on radio listeners, and found this website. I can’t figure out over what period their “cume” listeners were measured (reached out to them and never heard back). Do any of these figures ring a bell, or do you happen to know generally how long a span (1 week?) cume listeners are counted? [http://www.stationratings.com/sr\_ratings.aspx?market\=51](http://www.stationratings.com/sr_ratings.aspx?market=51)
		
		
		[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=643&_wpnonce=819e2279f2)Like
67. **[Briefly « Stats Chat](https://www.statschat.org.nz/2020/01/29/briefly-282/)** says: 

[January 28, 2020 at 11:57 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-639) 


\[…] The Geography of FM Radio (via Nathan Yau on Twitter): spatial patterns of US radio stations. Some types follow population density; others strikingly don’t. \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=639&_wpnonce=725c64463b)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=639#respond)
69. **[AnyChart \| Coronavirus Cases, Radio Coverage, Animal Trade, and Job Growth — DataViz Weekly](https://www.anychart.com/blog/2020/01/31/coronavirus-cases-dataviz-weekly/)** says: 

[January 31, 2020 at 6:03 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-648) 


\[…] can find the Visualizing the Geography of FM Radio project on the personal website of Erin \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=648&_wpnonce=2e890887c0)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=648#respond)
71. **Rodger Collins** says: 

[February 11, 2020 at 8:48 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-658) 


Interesting — wish there were more detail I could zoom in on as I’m more interested in the signals themselves than what it looks like aesthetically on a map. I do have other resources though.


As far as Utah, without having those excruciating details I suspect it may have to do with terrain. Where I live n the Blue Ridge Mountains there’s maybe one FM station within 30 miles yet I can hear a station on almost every channel, in fact I regularly go to sleep listening to a classical station over 100 miles away on my clock radio. It’s because our elevation is so high that most of those signals have little or no obstruction in between. Given Utah’s extreme topographic variations I suspect this is a factor. Meanwhile the RabbitEars site tells me I have zero TV signals, which I already knew but confirmed. Too far away from any city and translator stations are very low power, at least for TV.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=658&_wpnonce=727512b14e)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=658#respond)
73. **[Visualizing the Geography of FM Radio \#Data \#Maps \#Radio \#Art « Adafruit Industries – Makers, hackers, artists, designers and engineers!](https://blog.adafruit.com/2020/02/26/visualizing-the-geography-of-fm-radio-data-maps-radio-art/)** says: 

[February 26, 2020 at 10:01 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-685) 


\[…] project from erindavis who “makes stuff with data.” These maps show the different ranges of broadcasting. \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=685&_wpnonce=6f9a14838f)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=685#respond)
75. **[spinjector](http://spinjector.wordpress.com)** says: 

[February 29, 2020 at 5:14 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-691) 


Sorry if this is a duplicate, I tried to comment already but it didn’t show up? This is a great project. I was a broadcast radio engineer for 20 years, and I wanted to do something like this, but the geographic data tools we have now didn’t exist back then. I wanted to point out an issue with this project: the maps don’t take into account the directionality of broadcast systems. They’re not always circular, and some can have complex patterns, like a jagged star or figure eight. Have you ever noticed that some AM broadcast sites have an array of towers spread across many acres of land? That’s because the towers interact to shape the broadcast pattern. This is mostly to protect other stations on the same frequency in a nearby region, but it can also focus more power in a particular direction, like into a population center. There are also issues with international treaties between the US and Canada. For FM stations, the pattern is created by the shape of the antenna way up on the tower, but AM stations can have many towers; the most I’ve ever seen is CFMJ\-640 in Grimsby Ontario, with 8 towers for one pattern. FM radio is generally line\-of\-sight and subject to local terrain, whereas AM radio is subject to a phenomenon known as tropospheric propagation, which basically means the signal bends around the curvature of the Earth (check wikipedia). This is also why AM stations lower their power at night; if they didn’t it would be a huge mess. Interference from solar radiation scrambles the signal during the day, but at night the troposphere settles down and the signals travel much further, all the way to the solar terminator. And sometimes all the way to the other side of the planet. There’s a hobby known as “dxing” where people have extremely sensitive receivers and extremely large antennas, and they basically sit up all night trying to find AM stations that are really far away (remember the movie Contact?). It’s most popular in Scandinavian countries, because they try to pick up stations in the US. And then they send a postcard or letter to say hi. Somewhere in a box I have a letter from a guy in Sweden, with pictures of his receiver rig \& 1000\-foot antenna, his dog, and some wild reindeer in his back yard. There’s a website I used for many years to refer to broadcast patterns called radio\[hyphen]locator\[dot]com. If you go there and look up a few stations I’m about to describe, you’ll see the directional patterns I’m speaking of. On the info page for FM stations, it has a link called “view coverage map”, and the AM stations have “view daytime coverage” and “view nighttime coverage”. I should explain these coverage maps are purely theoretical, based on the mathematics of the antenna design listed in the FCC license. This can be very informative, but they don’t take into account the real life shape of the pattern as measured on the ground. Doing field strength measurements of this nature is highly labor\-intensive, and only legally required for AM stations. If you look at the coverage map for KVOD\-FM in Denver, you’ll see it has a funky D\-shape that points to the east, with some jagged radials that point to the west. And the nighttime coverage for WBEN\-AM in Buffalo (home of the Buffalo Sabres!) is a figure eight pattern with the lobes oriented to the north \& south. There’s another tool I should mention, a plugin for the desktop version of Google Earth. You can download it free from Fccinfo\[dot]com, and it maps everything in the US, including TV, microwave links, and any FAA\-registered towers, regardless of what’s on them. It’s an awesome tool to play with.


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=691&_wpnonce=82c8c6ab8e)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=691#respond)
77. **[2020 weeknote 3 – radio, field recording, and running \| Paul Capewell](https://paulcapewell.com/2020/01/23/2020-weeknote-3/)** says: 

[May 28, 2020 at 5:14 am](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-783) 


\[…] I’m on the subject of radio, I saw this great visualisation of American FM stations from Erin Davis (via Robin Sloan) recently, which I \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=783&_wpnonce=78b93bd2c5)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=783#respond)
79. **[Local Solar Time \- GistTree](https://gisttree.com/reviews/local-solar-time/)** says: 

[October 24, 2020 at 9:40 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-1246) 


\[…] With radio and television other folks scheme care about what time assorted issues are going to be broadcast. On the assorted hand, they’re naturally geographically restricted: \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=1246&_wpnonce=3a4deee5c7)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=1246#respond)
81. **[Local Solar Time \- Your Cheer](https://your.cheer.id/2020/10/25/local-solar-time/)** says: 

[October 24, 2020 at 9:57 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-1247) 


\[…] With radio and television people do care about what time different things are going to be broadcast. On the other hand, they are naturally geographically limited: \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=1247&_wpnonce=6f30c86b7a)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=1247#respond)
83. **[Local Solar Time \| صحافة حرة FREE PRESS](https://free-pres.com/2020/10/local-solar-time/)** says: 

[October 25, 2020 at 2:24 pm](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comment-1250) 


\[…] With radio and television people do care about what time different things are going to be broadcast. On the other hand, they are naturally geographically limited: \[…]


[Like](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?like_comment=1250&_wpnonce=fd186e3296)Like



[Reply](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/?replytocom=1250#respond)



### Leave a comment [Cancel reply](/2020/01/04/visualizing-the-geography-of-fm-radio/#respond)





Δ

 





Follow Blog via Email
---------------------




Enter your email address to follow this blog and receive notifications of new posts by email.




 Email Address: 
 








 
 Follow 





Social Media
------------


* [Instagram](https://www.instagram.com/erindataviz/)
* [Twitter](https://twitter.com/erindataviz)
* [GitHub](https://github.com/erdavis1)


Search
------



Search for:



 




[Blog at WordPress.com.](https://wordpress.com/?ref=footer_blog)





















































































* [Comment](https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/#comments)
* Reblog
* Subscribe
Subscribed




	+ [![](opensource/tidytuesday/2022-11-08/images/10.png) Data Stuff](https://erdavis.com)
Join 467 other subscribers







 

 Sign me up 


* Already have a WordPress.com account? [Log in now.](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Fr-login.wordpress.com%2Fremote-login.php%3Faction%3Dlink%26back%3Dhttps%253A%252F%252Ferdavis.com%252F2020%252F01%252F04%252Fvisualizing-the-geography-of-fm-radio%252F)
* [Privacy](#)
* + [![](opensource/tidytuesday/2022-11-08/images/10.png) Data Stuff](https://erdavis.com)
	+ [Customize](https://erdaviscom.wordpress.com/wp-admin/customize.php?url=https%3A%2F%2Ferdaviscom.wordpress.com%2F2020%2F01%2F04%2Fvisualizing-the-geography-of-fm-radio%2F)
	+ Subscribe
	Subscribed
	+ [Sign up](https://wordpress.com/start/)
	+ [Log in](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Fr-login.wordpress.com%2Fremote-login.php%3Faction%3Dlink%26back%3Dhttps%253A%252F%252Ferdavis.com%252F2020%252F01%252F04%252Fvisualizing-the-geography-of-fm-radio%252F)
	+ [Copy shortlink](https://wp.me/paqxBo-6f)
	+ [Report this content](https://wordpress.com/abuse/?report_url=https://erdavis.com/2020/01/04/visualizing-the-geography-of-fm-radio/)
	+ [View post in Reader](https://wordpress.com/read/blogs/154089058/posts/387)
	+ [Manage subscriptions](https://subscribe.wordpress.com/)
	+ Collapse this bar






 





























































Loading Comments...



 


Write a Comment...




Email (Required)



Name (Required)



Website











### 

























 


%d 



 





































































































































































































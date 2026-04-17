Adventures in Barstool’s Pizza Data \| by Tyler Richards \| Towards Data Science[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F9b8ae6bb6cd1&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderCollection&source=---top_nav_layout_nav----------------------------------)[Sign up](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Write](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fnew-story&source=---top_nav_layout_nav-----------------------new_post_topnav-----------)[Sign up](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

Adventures in Barstool’s Pizza Data
===================================

[Tyler Richards](https://tylerjrichards.medium.com/?source=post_page---byline--9b8ae6bb6cd1--------------------------------)

·[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Ffd6b02116248&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&user=Tyler+Richards&userId=fd6b02116248&source=post_page-fd6b02116248--byline--9b8ae6bb6cd1---------------------post_header-----------)

Published in[Towards Data Science](https://towardsdatascience.com/?source=post_page---byline--9b8ae6bb6cd1--------------------------------)·7 min read·May 11, 2019\-\-

Listen

Share

\[Want to see more Data Science projects? Check out [my website](http://www.tylerjrichards.com/) or my [twitter](https://twitter.com/tylerjrichards)]

![]()

New York Pizza Reviews

In January, I moved to NYC to spend 6 months doing non\-profit data science work, without ever having stepped foot in any of the 5 boroughs. People here take their pizza extremely seriously, and so I wanted to eat the best before I’m stuck with even higher priced rent and worse pizza (San Fran).

The rest of this piece is a statistical analysis of NYC pizza data (scraped from a website called Barstool), which includes reverse engineering APIs, fun maps, and stats techniques I haven’t had a good reason to try before. (If you just want to see the graphs or play around with the maps, scroll down until you see another map). Because I have limited time in NYC, I needed to aggressively prioritize. But when you google ‘best pizza in NYC’, you’ll get either thousands of lists all reviewed by different people, or you can get aggregated pseudo\-anonymous reviews on websites like Yelp or OpenTable.

But none of these options would truly work for a good quality estimate. Is there a better way to think about this problem? The data isn’t great from Yelp/OpenTable because those consumers only review restaurants they’re already going to, and the platforms themselves [filter out reviews](https://marketingland.com/yelp-more-likely-to-filter-extreme-reviews-new-accounts-study-53622). Not to mention that one person’s 4/5 star rating is probably not the same as another’s, severely biasing aggregates. No chance there. I could aggregate the curated lists and look for trends, but how much more does being 4th on Eataly’s list matter than 1st on ‘adventurous NYC tourist’s’ blog? This is not clear (and I would rather not scrape a hundred different websites if I can get around it, let’s be honest it’s mostly that).

The best case scenario would be for a person to have to randomly go to a pizza place and review it with a scale granular enough to get a probability density. Doing this enough times will allow us to understand what an 8\.2/10 ***really*** means. An 8\.2 could be garbage if the average review was 9\.7/10, or it could be amazing if that average was, say, a 5/10\.

The Search
----------

With this in mind, I went searching for a good dataset of pizza reviews. I stumbled on what seems like a gold mine, Barstool’s [Dave Portnoy](https://www.instagram.com/stoolpresidente/). Dave reviews a pizza place every day in NYC and posts those reviews on Instagram and on their mobile app One Bite (watch a few of their reviews if you have a minute, they’re boisterous but they take pizza seriously). I excitedly emailed them, asking for access to their data. But, as expected, they don’t want to give read access to their database to a random data scientist. I was on my own.

Reverse Engineering
-------------------

Their pizza data sits in two places, on [Instagram](https://www.instagram.com/p/Bwc_r_Wh0JY7_o6E6bLBRcEVrpvSWG2An7hT8o0/) and on their mobile\-only app called One Bite (shown below).

![]()For Instagram scraping, I could either hire Mechanical Turk workers to listen to each review and put that into a database or do that myself. Given that there are hundreds of reviews, and the glaring [ethical problems](https://www.theatlantic.com/business/archive/2018/01/amazon-mechanical-turk/551192/) with it, Mechanical Turk wasn’t an option.

What if I could record the web traffic coming through the application, and reverse engineer their API instead? I found an application called [charles](https://www.charlesproxy.com/), which pushes web traffic to an iPhone to help app developers debug more efficiently. If I could use it for a slightly different purpose and siphon my iPhone’s web traffic through charles as I was using the app, I could try to reverse engineering their API. It turns out, this worked fantastically well (we sit on the shoulders of the giants who make [internet tutorials](http://www.testeffective.com/better-mobile-app-testing-with-charles-proxy/)). They have a [venue endpoint](https://one-bite-api.barstoolsports.com/venue) that, when hit, returns an amazing amount of data including names and locations of the venue, along with scores from the community basically get read access to their database.

The endpoint had abysmal security having no verification process on the server or device side and was queryable based on location, store type, and any other feature in the data. The only issue is that the endpoint returns a maximum of 50 locations, but I got around this by randomly generating 10,000 locations around the United States and using those as inputs to the query string, successfully getting 463 pizza reviews.

The Data
--------

These data had everything. The review score that Dave gave the location, the community’s score, the name of the pizza joint. Even the link to the thumbnail used in the application, and links to the AWS s3 buckets where all the media was kept (fyi: not the best idea to do this). Finally. The only missing fields I needed for geographic mapping were longitude and latitude so I used the [Google maps reverse geocoder](https://developers.google.com/maps/documentation/geocoding/start) to get that information as well. I’ve put all the data in [this GitHub repo](https://github.com/tylerjrichards/Barstool_Pizza) for anyone to mess around with.

First, I wanted to figure out where the best pizza was clustered around. Are certain areas better at making pizza than others within New York? I used kepler (Uber’s open source geographic visualization framework) to get the clusters of reviewed pizza locations with the best scores and hosted the interactive map [here](http://www.tylerjrichards.com/pizza_map.html) as a sandbox for anyone to analyze. There are some really great pizza clusters around NYU and around SoHo, along with Williamsburg in Brooklyn.

![]()Please feel free to get on a play around with this data inside kepler (or anywhere else), visualizing pizza data is truly wonderful.

Data Exploration
----------------

Before we get to the questions about data distribution, where is our sample generated from? The assumption is that the reviews are mostly from word of mouth recommendations and that the sheer size of the reviews by a single person will lend itself toward a more nuanced analysis of pizza reviews.

![]()The overwhelming number of pizza reviews happened in New York, coming in at about 250 reviews in Manhattan alone (another 20 or so from Brooklyn, and a smattering of reviews in Vegas, Miami, etc). No other city even gets to 20 reviews. If we look at the top few cities by review count, we get an idea about why a large number of reviews are necessary to judge quality.

![]()For New York, the number of reviews is high enough to start to approach a more recognizable distribution than with other cities (this is expected with larger samples). I would guess that each city has it’s own true distribution of pizza quality, and a small sample is more likely to have cherry\-picked examples that tell us little about actual quality. The median review score for all the data is 7\.1, with a standard deviation of 1\.78\. 3 of the top 5 pizza places in the dataset are in New York, and a couple of weeks ago I made my way to the best pizza joint (Di Fara) and, even though it took 2 hours to get a slice, it was well worth it. See the rest of the top 5 below.

![]()How good is 8\.1?
-----------------

The next question I had was a little more technical. What is the underlying density of pizza scores? How much better is an 8\.1 vs a 9\.5? Just knowing the median isn’t nearly good enough. Again, I thought of the individual data scores as samples from some distribution of true quality perception. Then, I used a kernel density estimator to estimate this probability density function. In layman’s terms, a KDE is a way to comprehend the whole of the data without making many assumptions. In this data, I didn’t want to assume that data was centered around any point (say, assume that most of the reviews were around 5\), or that it was spread out evenly. There is an [excellent blog post](https://mathisonian.github.io/kde/) on KDE’s that will probably give better intuition than most university classes, and a more difficult, but still quite good, [paper](https://arxiv.org/pdf/1704.03924.pdf) describing this method. Scipy has a wonderful method to both compute the KDE, and to sample from it.

![]()

Fitting the Gaussian KDE

Once I fit this density, I sampled from it to get a more robust dataset. The density histogram is below. With this, I could estimate if a single pizza location is in the top x% of NYC locations in a much more significant way than simple counting from the application’s data.

![]()

Histogram of Pizza Reviews with KDE

This dataset also included the pizza ratings of application users. I used the same method as before to estimate the density of the community and graphed both below.

![]()The application’s users tend to follow the same density as Portnoy, with significantly more reviews around 0 (a harsh bunch), but also more above the median. This generally follows my hypothesis from earlier that reviewers are more polarized in their reviews.

Fin
---

These data were equally difficult to get and fun to play around with, please reach out to me at tylerjrichards@gmail.com or on [here](http://www.tylerjrichards.com/) if you have any questions about anything done above!

Other not completed but potentially fun projects to do on these data are predicting pizza reviews by location and price, creating a recommendation algorithm for similar pizza shops, and mapping the closest good pizza spot by subway stop.

[Data Science](https://medium.com/tag/data-science?source=post_page-----9b8ae6bb6cd1--------------------------------)[Food](https://medium.com/tag/food?source=post_page-----9b8ae6bb6cd1--------------------------------)[Pizza](https://medium.com/tag/pizza?source=post_page-----9b8ae6bb6cd1--------------------------------)[Barstool Sports](https://medium.com/tag/barstool-sports?source=post_page-----9b8ae6bb6cd1--------------------------------)\-\-

\-\-

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Ffd6b02116248&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&user=Tyler+Richards&userId=fd6b02116248&source=post_page-fd6b02116248--post_author_info--9b8ae6bb6cd1---------------------follow_profile-----------)[Written by Tyler Richards
-------------------------](https://tylerjrichards.medium.com/?source=post_page---post_author_info--9b8ae6bb6cd1--------------------------------)[144 Followers](https://tylerjrichards.medium.com/followers?source=post_page---post_author_info--9b8ae6bb6cd1--------------------------------)·Writer for [Towards Data Science](https://towardsdatascience.com/?source=post_page---post_author_info--9b8ae6bb6cd1--------------------------------)DS @ FB

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Ffd6b02116248&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fadventures-in-barstools-pizza-data-9b8ae6bb6cd1&user=Tyler+Richards&userId=fd6b02116248&source=post_page-fd6b02116248--post_author_info--9b8ae6bb6cd1---------------------follow_profile-----------)[Help](https://help.medium.com/hc/en-us?source=post_page-----9b8ae6bb6cd1--------------------------------)[Status](https://medium.statuspage.io/?source=post_page-----9b8ae6bb6cd1--------------------------------)[About](https://medium.com/about?autoplay=1&source=post_page-----9b8ae6bb6cd1--------------------------------)[Careers](https://medium.com/jobs-at-medium/work-at-medium-959d1a85284e?source=post_page-----9b8ae6bb6cd1--------------------------------)[Press](pressinquiries@medium.com?source=post_page-----9b8ae6bb6cd1--------------------------------)[Blog](https://blog.medium.com/?source=post_page-----9b8ae6bb6cd1--------------------------------)[Privacy](https://policy.medium.com/medium-privacy-policy-f03bf92035c9?source=post_page-----9b8ae6bb6cd1--------------------------------)[Terms](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----9b8ae6bb6cd1--------------------------------)[Text to speech](https://speechify.com/medium?source=post_page-----9b8ae6bb6cd1--------------------------------)[Teams](https://medium.com/business?source=post_page-----9b8ae6bb6cd1--------------------------------)




























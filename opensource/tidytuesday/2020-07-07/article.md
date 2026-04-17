Where can you find the best coffee? \| by Yorgos Askalidis \| Medium[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F91f88ed37e84&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderUser&source=---top_nav_layout_nav----------------------------------)Sign up

[Sign in](/m/signin?operation=login&redirect=https%3A%2F%2Fmedium.com%2F%40yaskalidis%2Fthe-data-speak-ethiopia-has-the-best-coffee-91f88ed37e84&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Write](/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fnew-story&source=---top_nav_layout_nav-----------------------new_post_topnav-----------)Sign up

[Sign in](/m/signin?operation=login&redirect=https%3A%2F%2Fmedium.com%2F%40yaskalidis%2Fthe-data-speak-ethiopia-has-the-best-coffee-91f88ed37e84&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

Where can you find the best coffee?
===================================

[Yorgos Askalidis](/@yaskalidis?source=post_page---byline--91f88ed37e84--------------------------------)

·[Follow](/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2F2c4731836156&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40yaskalidis%2Fthe-data-speak-ethiopia-has-the-best-coffee-91f88ed37e84&user=Yorgos+Askalidis&userId=2c4731836156&source=post_page-2c4731836156--byline--91f88ed37e84---------------------post_header-----------)

6 min read·Mar 26, 2019\-\-

3

Listen

Share

The world loves coffee! It is one of the world’s most traded commodities and it can excite our senses with its plethora of great aromas and flavors. In this blog post we’re gonna get a glimpse on the professional practice of grading coffee samples and try to understand what makes for a great coffee.

*What country produces that coffee with the best aroma?*

*Does altitude affect the overall quality of the coffee?*

*Can we build a coffee profile for various countries?*

*Do professional graders tend to score lower or Mondays?*

I analyzed a dataset containing professional grades for 1,300 Arabica coffee samples from around the world to answer all the above questions.

From the wiki page for [coffee cupping](https://en.wikipedia.org/wiki/Coffee_cupping).


> **Coffee cupping**, or **coffee tasting**, is the practice of observing the tastes and aromas of brewed coffee. It is a professional practice but can be done informally by anyone or by professionals known as “Q Graders”.

![]()The [Coffee Quality Institute](https://www.coffeeinstitute.org/) is a non\-profit organization that grades coffee samples from around the world in a consistent and professional manner. The result are published on their website and were scraped by reddit user [JLD](https://www.reddit.com/user/JLD_) and posted on the forum’s [dataset community.](https://www.reddit.com/r/datasets/comments/8rndor/data_on_1340_coffee_bean_reviews_aroma_acidity/)

The dataset contains the grades the cuppers gave a sample on each of these ten attributes: *Aroma, Flavor, Aftertaste, Acidity, Body, Balance, Uniformity, Clean Cup, Sweetness, Cupper Points.*

Each grade is on a 0–10 scale resulting to a total cupping score between zero and one hundred. If you want to get more familiar with the 100\-point scale coffee review process you can take a look at [this article](http://cafevirtuoso.com/2017/09/12/what-you-need-to-know-about-the-coffee-review-100-point-scale/) and if you want to understand better what **exactly** each attribute is you can read the explanations [here](https://database.coffeeinstitute.org/coffee/976032/grade).

Building each country’s coffee profile
--------------------------------------

The dataset records each coffee sample’s country of origin, and that allows me to aggregate the grades for each country and build that country’s *coffee profile*. Figure 1 shows the results for a few countries and one thing that becomes pretty apparent is that there is actually not much variation between countries! If you look really closely you might notice that e.g., Ethiopia seems to have higher grades than most other countries but not much a large margin. To exemplify this further, the median score on uniformity, clean cup and sweetness is a perfect ten for almost every country.

![]()

**Figure 1:** Radar plots with the average score for each country and attribute.

Figure 2 shows all the profiles together to showcase once again how there is not too much difference.

![]()

**Figure 2:** The taste profile of all 19 countries with at least 10 coffee samples. Each point of the polygon represents the **average score** of each country for that characteristic.

With the taste profiles of each country being not too distinct from each other, let’s see which country’s coffee samples scored the highest in each category. Note that for this analysis, I’m restricting the ranking only to the 19 countries that have at least 10 coffee samples graded. Additionally, I am taking the **median grade** of each country’s coffee samples for every category, because it is a more robust metric compared the average.

Highest Ranked Country, and runner up
-------------------------------------

1. **Aroma:** Uganda (7\.92\), Kenya (7\.83\)
2. **Flavor:** Ethiopia (7\.96\), Kenya (7\.83\)
3. **Aftertaste:** Ethiopia (7\.83\), Kenya (7\.75\)
4. **Acidity:** Ethiopia (8\.0\), Kenya (7\.75\)
5. **Body:** Ethiopia (7\.92\), Peru (7\.92\)
6. **Balance:** Ethiopia (7\.92\), Kenya (7\.75\)
7. **Uniformity:** All countries tied with a score of 10
8. **Clean Cup:** All countries tied with a score of 10
9. **Sweetness:** All countries tied with a score of 10
10. **Cupper Points:** Ethiopia (8\.0\), Kenya (7\.83\)

We observe that Ethiopia ranks the highest (including ties) in 9 out of 10 areas of grading. Kenya is the most frequent runner\-up.

**Out of the ten highest graded coffee samples, seven were from Ethiopia.** That included the top two. Guatemala, Brazil and Peru had one appearance each.

*Next time I’m getting a coffee, I’ll be on the lookout for bag from Ethiopia!*

Analyzing additional coffee characteristics
-------------------------------------------

The dataset also includes some information about the coffee sample’s **altitude** of origin, **variety**, **processing method** and **color**. I examine here if any of these characteristics correlate with the total cupping score.

A statistical analysis of the relationship between the **altitude** of the sample and its total cupping score found **no significant correlation**. I don’t really know enough to be surprised or not by this finding. Are there any coffee experts out there that (formally or informally) have found any links between altitude and coffee quality?

The **processing method** can be one of Natural/Dry, Pulped Natural/Honey, Semi\-washed/Semi\-Pulped, Washed/Wet, Other and None. The **color** of the coffee sample can be Blueish Green, Blue Green, Green and None. And the **variety** of the sample can be one of many options including such as Blue mountain, Bourbon, Catimor, Caturra and more.

OLS and Kolmogorov\-Smirnov test analysis did not uncover any strong statistically significant correlations between any one of the aforementioned characteristics and the total cupping score of the coffee sample.

BONUS: Do graders give lower scores on Mondays?
-----------------------------------------------

![]()

**Figure 3:** Median total score per grading year, month and day of week. The opacity of the bars on the left\-hand plots are proportional to the number of grading that happened that year, month and day of week (shown on the right\-hand side plots)

Shifting focus away from the coffee samples, I wanted to take a look at the grading **date**. There is research that has [found correlation between a parole case’s success rate and whether the case was heard right before or after lunch](https://www.wired.com/2011/04/judges-mental-fatigue/). The idea here is that judges might simply be a in a better mood right after lunch. I wanted to see if there is any evidence of something like that happening with the coffee sample grading: Do graders give higher or lower grades on a Friday compared to a Monday?

**The answer seems to be No.**

There is no statistical difference between the grades that are awarded on a Monday compared to a Friday or any other day of the week. If you look at the third plot in Figure 3 you will see that the median grade on Fridays seems to be a little higher compared to other days but a statistical analysis revealed no correlation. I performed a 2\-sample Kolmogorov\-Smirnov test between the grades awarded on a Monday and those awarded on a Friday and found no statistical difference. I also performed a regular OLS regression and still found no correlation.

Beyond the day of the week, Figure 2 shows that June is the busiest month for grading and that 2012 was a particularly busy (and low\-grade!) year. As was the case with various days of the week, there were no statistical differences between the grades awarded on various months of the year.

There *were* statistical differences across the grading years but those cannot be easily attributed to the graders; inherent factors about the coffee crops might have a much a bigger influence.

So there you have it, Ethiopia has the highest graded coffee samples recorded in the dataset and is consistently the highest ranked on almost all the individual stages of the cupping.

As a bonus exploration, coffee graders seem to be consistent with their grading across years, months and days of the week.

If all this talk about coffee got you in the mood for a cup of joe and some tunes, you can also read [Spotify’s blog post](https://newsroom.spotify.com/2019-03-20/how-to-find-the-perfect-playlist-for-your-coffee-break-vibe/) about coffee inspired playlists.

*Are you a professional or amateur coffee cupper? Do these results surprise you? Let me know your thoughts and experiences in the comments!*

[Coffee](/tag/coffee?source=post_page-----91f88ed37e84--------------------------------)[Data](/tag/data?source=post_page-----91f88ed37e84--------------------------------)[Data Analysis](/tag/data-analysis?source=post_page-----91f88ed37e84--------------------------------)[Data Visualization](/tag/data-visualization?source=post_page-----91f88ed37e84--------------------------------)[Ethiopia](/tag/ethiopia?source=post_page-----91f88ed37e84--------------------------------)\-\-

\-\-

3

Follow[Written by Yorgos Askalidis
---------------------------](/@yaskalidis?source=post_page---post_author_info--91f88ed37e84--------------------------------)[199 Followers](/@yaskalidis/followers?source=post_page---post_author_info--91f88ed37e84--------------------------------)Data Scientist at Instagram NYC. Previously at Spotify. Ask me about data, soccer, or data about soccer (or anything else).

Follow[Help](https://help.medium.com/hc/en-us?source=post_page-----91f88ed37e84--------------------------------)[Status](https://medium.statuspage.io/?source=post_page-----91f88ed37e84--------------------------------)[About](/about?autoplay=1&source=post_page-----91f88ed37e84--------------------------------)[Careers](/jobs-at-medium/work-at-medium-959d1a85284e?source=post_page-----91f88ed37e84--------------------------------)[Press](pressinquiries@medium.com?source=post_page-----91f88ed37e84--------------------------------)[Blog](https://blog.medium.com/?source=post_page-----91f88ed37e84--------------------------------)[Privacy](https://policy.medium.com/medium-privacy-policy-f03bf92035c9?source=post_page-----91f88ed37e84--------------------------------)[Terms](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----91f88ed37e84--------------------------------)[Text to speech](https://speechify.com/medium?source=post_page-----91f88ed37e84--------------------------------)[Teams](/business?source=post_page-----91f88ed37e84--------------------------------)



























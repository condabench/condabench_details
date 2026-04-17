Great American Coffee Taste Test Breakdown \| by Robert McKeon Aloe \| Medium[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F7f3fdcc3c41d&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderUser&source=---top_nav_layout_nav----------------------------------)Sign up

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Frmckeon.medium.com%2Fgreat-american-coffee-taste-test-breakdown-7f3fdcc3c41d&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Write](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fnew-story&source=---top_nav_layout_nav-----------------------new_post_topnav-----------)Sign up

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Frmckeon.medium.com%2Fgreat-american-coffee-taste-test-breakdown-7f3fdcc3c41d&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

Coffee Data Science
-------------------

Great American Coffee Taste Test Breakdown
==========================================

Looking at the rich dataset as the result of James Hoffmann’s taste test
------------------------------------------------------------------------

[Robert McKeon Aloe](/?source=post_page---byline--7f3fdcc3c41d--------------------------------)

·[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fae592466d35f&operation=register&redirect=https%3A%2F%2Frmckeon.medium.com%2Fgreat-american-coffee-taste-test-breakdown-7f3fdcc3c41d&user=Robert+McKeon+Aloe&userId=ae592466d35f&source=post_page-ae592466d35f--byline--7f3fdcc3c41d---------------------post_header-----------)

6 min read·Nov 28, 2023\-\-

Listen

Share

In October 2023, James Hoffmann did a livestream taste test with around 4,000 people in the USA. A month later, he released the survey data! I love data, so I went through the data and pulled what I thought were interesting statistics. This article is heavy in data and charts; beware. You can also download the raw and repeat any of this analysis.

For the taste test, every participant was sent four coffee samples without labels. People brewed them, recorded notes, and answered questions on preference. Hopefully, this was during the livestream where James then revealed what the coffees were.

This data was very rich in the demographics and the questions related to coffee and the taste test. I excluded data where the number of responses was too small. For example, the number of people under 18 was too low for most data cuts.

**Data Caveats:**

1. This data was volunteer data.
2. Not everyone who did the tasting filled out every question.
3. This is a sample of people who are fans of James Hoffmann and were able to participate in the tasting

Who, What, Where, How, Why?
===========================

Most people brew at home, and far fewer brew elsewhere.

![]()

All images by author

Pour\-over and Espresso were the top two categories, but we can also see what people brew multiple types.

![]()This matrix shows how many people brew both what’s in the column and the row. So 27% of people who make pour\-over also make espresso. The blank spaces are below 0\.5%.

![]()When people buy coffee, most in this survey bought from a specialty shop.

![]()Most people in this group did not add anything to their coffee.

![]()For the milk, people added mostly added whole milk, but many used oat milk. Many didn’t add any milk.

![]()For sugar, most used regular sugar if any at all.

![]()Almost everyone drinks coffee because it tastes good, but some have other reasons.

![]()Of the people who don’t drink coffee for the taste, I broke down their reasons for drinking coffee. Multiple answers could be selected.

![]()Then we can look at a cross matrix of reasons why people drink coffee.

![]()Taste Preferences
=================

Here are a bunch of breakdowns on roast preferences based on who preferred what starting with people who preferred different coffees. Coffees A, B, and C are the same Kenyan beans roasted light, medium, and dark. Coffee D was a coffee bean from Colombia using experimental processing giving it more fruity and ferment flavors. I put Coffee D above A because I felt like the coffee was closer to A than the other coffees.

![]()A quick detour to look at how much coffee different age brackets drink. I wonder if the weight of coffee would have said something different.

![]()There were some preferences amongst states. This is sorted by number of responses where each state had at least 90 responses. The challenge was that at 90 responses, just a few preferred dark roasts.

![]()Political affiliation was included, and while I was hopeful there was something more interesting, the slight preference to Medium/Dark roasts by Republicans could be skewed because of age.

![]()Here is the politics by age of this cohort showing a shift in affiliation around 55 years old.

![]()Age seems to play a part in roast level preferences:

![]()This probably explains the political plot more than anything else.

Moving on to Gender, there is a big difference between male and female preferences. I wonder if coffee shops take that into account or if coffee shops predominately run by men or women have different roast preferences.

![]()Relationship status seems to suggest by getting a divorce, you go darker on your roast preferences.

![]()This could be conflated with age like politics, but the counts of divorce per age bracket are pretty even. However, the bin sizes are low at this point.

![]()This trend stays true for the actual tasting of coffees A, B, C, and D.

![]()Does the number of kids influence how dark you like your coffee? Maybe there is a trend?

![]()There are differences amongst ethnicities, and these are the ones that had enough data to plot.

![]()Money
=====

We coffee people can spend a lot on coffee. Is there a tie\-in with roast preference? It seems lighter roasts are more preferred as more money is spent.

![]()I compared Annual Income to roast preference. A slight trend towards lighter roasts, but not much.

![]()I crossed this data with Annual Income to understand how much people are willing to spend on coffee. It is surprisingly even all things considered.

![]()How much would you pay for a cup? Most won’t pay a ton for darker roasts.

![]()Now we can cross Annual Income with the most you would pay for coffee. This is also surprisingly even.

![]()What do all these metrics mean? Whatever you make of them. Maybe you can craft a more unique coffee experience for people by better understanding and appreciating the differences in tastes amongst the many variables of people as compared to the many variables of coffee.

I would be curious for something like this to be done in other countries, but maybe marketing companies already have this type of data.

The one critique I have is that Kenyan beans can be difficult to roast and brew compare to others. I would have chosen a Colombian or Ethiopian bean, but then again I was designing the study.

If you like, follow me on [Twitter](https://mobile.twitter.com/espressofun), [YouTube](https://m.youtube.com/channel/UClgcmAtBMTmVVGANjtntXTw), and [Instagram](https://www.instagram.com/espressofun/) where I post videos of espresso shots on different machines and espresso related stuff. You can also find me on [LinkedIn](https://www.linkedin.com/in/dr-robert-mckeon-aloe-01581595). You can also follow me on [Medium](https://towardsdatascience.com/@rmckeon/follow) and [Subscribe](/subscribe).

[Further readings of mine](/story-collection-splash-page-e15025710347):
=======================================================================

[My Second Book: Advanced Espresso](https://www.kickstarter.com/projects/espressofun/advanced-espresso-elements-of-coffee-extraction)

[My First Book](https://www.kickstarter.com/projects/espressofun/engineering-better-espresso-data-driven-coffee): Engineering Better Espresso

[My Links](/my-links-5de9eb69c26b)

[Collection of Espresso Articles](/a-collection-of-espresso-articles-de8a3abf9917?postPublishedType=repub)

[A Collection of Work and School Stories](/a-collection-of-work-and-school-stories-6b7ca5a58318)

[Coffee Data Science](https://medium.com/tag/coffee-data-science?source=post_page-----7f3fdcc3c41d--------------------------------)[Coffee](https://medium.com/tag/coffee?source=post_page-----7f3fdcc3c41d--------------------------------)[Espresso](https://medium.com/tag/espresso?source=post_page-----7f3fdcc3c41d--------------------------------)[Data](https://medium.com/tag/data?source=post_page-----7f3fdcc3c41d--------------------------------)[Data Science](https://medium.com/tag/data-science?source=post_page-----7f3fdcc3c41d--------------------------------)\-\-

\-\-

Follow[Written by Robert McKeon Aloe
-----------------------------](/?source=post_page---post_author_info--7f3fdcc3c41d--------------------------------)[2K Followers](/followers?source=post_page---post_author_info--7f3fdcc3c41d--------------------------------)I’m in love with my Wife, my Kids, Espresso, Data Science, tomatoes, cooking, engineering, talking, family, Paris, and Italy, not necessarily in that order.

Follow[Help](https://help.medium.com/hc/en-us?source=post_page-----7f3fdcc3c41d--------------------------------)[Status](https://medium.statuspage.io/?source=post_page-----7f3fdcc3c41d--------------------------------)[About](https://medium.com/about?autoplay=1&source=post_page-----7f3fdcc3c41d--------------------------------)[Careers](https://medium.com/jobs-at-medium/work-at-medium-959d1a85284e?source=post_page-----7f3fdcc3c41d--------------------------------)[Press](pressinquiries@medium.com?source=post_page-----7f3fdcc3c41d--------------------------------)[Blog](https://blog.medium.com/?source=post_page-----7f3fdcc3c41d--------------------------------)[Privacy](https://policy.medium.com/medium-privacy-policy-f03bf92035c9?source=post_page-----7f3fdcc3c41d--------------------------------)[Terms](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----7f3fdcc3c41d--------------------------------)[Text to speech](https://speechify.com/medium?source=post_page-----7f3fdcc3c41d--------------------------------)[Teams](https://medium.com/business?source=post_page-----7f3fdcc3c41d--------------------------------)



























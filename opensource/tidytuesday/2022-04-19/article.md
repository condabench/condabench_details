The Wild World of Crossword Data. I’ve always been pretty into… \| by Kurt Reckziegel \| Towards Data Science[Open in app](https://rsci.app.link/?%24canonical_url=https%3A%2F%2Fmedium.com%2Fp%2F71d560e222f5&%7Efeature=LoOpenInAppButton&%7Echannel=ShowPostUnderCollection&source=---top_nav_layout_nav----------------------------------)[Sign up](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Write](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fnew-story&source=---top_nav_layout_nav-----------------------new_post_topnav-----------)[Sign up](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

[Sign in](https://medium.com/m/signin?operation=login&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&source=post_page---top_nav_layout_nav-----------------------global_nav-----------)

The Wild World of Crossword Data
================================

[Kurt Reckziegel](https://medium.com/@kurtreckz?source=post_page---byline--71d560e222f5--------------------------------)

·[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fe24da3221b06&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&user=Kurt+Reckziegel&userId=e24da3221b06&source=post_page-e24da3221b06--byline--71d560e222f5---------------------post_header-----------)

Published in[Towards Data Science](https://towardsdatascience.com/?source=post_page---byline--71d560e222f5--------------------------------)·5 min read·Feb 23, 2018\-\-

1

Listen

Share

![]()

Photo by [Natalia Ostashova](https://unsplash.com/photos/cWhLlFB2IGI?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

I’ve always been pretty into crosswords. My mom and sisters would pull the New York Times Crossword out of the Montreal Gazette and work on it together, sometimes throwing a sports\-related question my way.

Fast\-forward to 30\+ Kurt, and now I’m solving full puzzles on my own, like a real boy. When I really got into it though, was over the most recent Christmas holiday, when the temperature outside was a brisk \-31°F at our lakehouse on Lac Pilon in Sainte\-Adèle. Needless to say, we spent most days inside by a crackling fire sipping something warm. Despite the cold, it was a delightful holiday, and with no cable (and pretty spotty wifi) we passed the time doing crosswords.

Now, back in NYC, where the weather is a little less arctic, I consider myself a full\-blown puzzle\-fiend, and I get my fix in a few different ways:

* Since she still gets an actual newspaper delivered to her door every morning, my lovely mother is kind enough to scan and email each and every NYT Crossword to my girlfriend and me (which we promptly print out and add to the growing stack on our dedicated crossword clipboard).
* I paid for a digital subscription to the NYT (I know, crazy, right?) just to get access to their crosswords. Yeah, this does duplicate what mom sends, but it also gives me access to the daily minis, which are perfect for the subway commute.
* Speaking of subway commutes, mine’s pretty long. So if I don’t have any minis left to do, I sometimes get to scratch my crossword itch by solving a couple clues in my head while peeking at someones Metro puzzle over their shoulder (creepy or resourcful?).
What’s the big deal about the NYT Crossword anyway?
---------------------------------------------------

I’m paraphrasing from [Wikipedia](https://en.wikipedia.org/wiki/The_New_York_Times_crossword_puzzle) here, but basically it’s a daily puzzle published by the New York Times and also syndicated to over 300 other newspapers and publications (which is how my mom gets it in Montreal).

It’s got a whole slew of different contributors, but since 1993 has always been edited by good ol’ Will Shortz. Every day of the week the puzzle gets progressively harder, with the easiest being Monday and hardest Saturday (Sundays are a larger puzzle and usually equated to about the same difficulty as a Thurdsay). Over time, I’ve gotten pretty comfortable with Mondays and Tuesdays, but still have some trouble finishing a whole Wednesday puzzle.

Enough about history, let’s talk data
=====================================

Thanks to [michael](https://medium.com/u/82d1ce446ee1?source=post_page---user_mention--71d560e222f5--------------------------------), I was able to get my hands on a decently sized [data dump](https://github.com/donohoe/nyt-crossword) that includes NYT Crossword data from December 1993 to July 2017\. What did I do next? Well, first I put down the Wednesday crossword I was working on, and then I dove right in.

After uploading the data into Google Cloud, and running some SQL queries on it in BigQuery, here are a few fun facts I found:

Fun Facts
---------

* 24\.5 years
* 8,238 puzzles
* 432,205 clues
* 108,423 unique answers
* 54,820 (or 51%) unique answers were never used more than once

Ok, so wait, that means **49% of all unique answers were used multiple times**?!

Hmmm interesting, I wonder which words are used most frequently…

Top 10 Most Used Answers Overall (\& Percent Puzzle Presence)
-------------------------------------------------------------

So, what have we got here? It looks like a set of short words that can easily be used to fill gaps left by longer answers. It’s also interesting to see the prominence of letters like ***E***, ***A***, and ***R***, since those are the three most frequently used letters in the English language (according to [Oxford Dictionaries](https://en.oxforddictionaries.com/explore/which-letters-are-used-most)). Those three letters combined account for 27\.24% of the English language, while for the NYT, they make up 68\.75% of the top 10 most used answers (22 out of 32 characters).

**Quick tip:** based on this data, you can probably expect the word ***ERA*** to show up about once every 2\.4 weeks. (Remember, the clue for this could be something related to time or baseball or equal rights.)

Curious to see how that looks broken down by day of the week? I got you.

Top 10 Most Used Answers by Day of Week
---------------------------------------

Something else I looked into was how long the clues were. I’ve found that they vary from being short, one\-word clues, to being much longer sentences or even paragraphs. Since the puzzle difficulty changes as the week progresses, I thought it may be cool to look at how the average clue character count changes throughout the week.

Average Clue Character Count by Day of Week
-------------------------------------------

Well, there it is, clear as day: *higher difficulty \= longer clues*

With the average character count increasing day\-over\-day from Wednesday to Saturday, we can confidently say that longer clues are usually harder clues. And, this may just be me, but I find it so satisfying that on Sunday the average character count drops back down to almost exactly the same level as Thursday (remember earlier I mentioned that Sundays are larger puzzles but are about the same level of difficulty as a Thursday).

The one thing I can’t explain is why there’s a slight drop in clue length from Monday to Wednesday. ***Anyone have any ideas??***

If you’ve ever worked on (or even looked at) a crossword, you know that there are clues and answers going in two directions: across and down. So, the last thing I looked into was whether there is a difference in clue lengths based on direction.

Average Clue Character Count by Answer Direction (\& Day of Week)
-----------------------------------------------------------------

Ok, this one didn’t pan out into much. Not a whole lot to look at here, but let’s try to stretch it into something. If we previously determined that longer clues usually mean harder clues, then based on the data above, could we say:

Down clues are easier than Across clues. ¯\\\_(ツ)\_/¯

Well, that’s all for today, folks. I’ve got to make some coffee and get back to this pesky Wednesday. Anyone know a six\-letter word for “joe”?

Tools Used
----------

Google Cloud Storage, Google BigQuery, Excel, GitHub, infogram

[Data](https://medium.com/tag/data?source=post_page-----71d560e222f5--------------------------------)[Sql](https://medium.com/tag/sql?source=post_page-----71d560e222f5--------------------------------)[Data Science](https://medium.com/tag/data-science?source=post_page-----71d560e222f5--------------------------------)[Language](https://medium.com/tag/language?source=post_page-----71d560e222f5--------------------------------)[Data Visualization](https://medium.com/tag/data-visualization?source=post_page-----71d560e222f5--------------------------------)\-\-

\-\-

1

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fe24da3221b06&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&user=Kurt+Reckziegel&userId=e24da3221b06&source=post_page-e24da3221b06--post_author_info--71d560e222f5---------------------follow_profile-----------)[Written by Kurt Reckziegel
--------------------------](https://medium.com/@kurtreckz?source=post_page---post_author_info--71d560e222f5--------------------------------)[188 Followers](https://medium.com/@kurtreckz/followers?source=post_page---post_author_info--71d560e222f5--------------------------------)·Writer for [Towards Data Science](https://towardsdatascience.com/?source=post_page---post_author_info--71d560e222f5--------------------------------)Working on consumer insights and brand strategy (alum of @onepeloton @abinbev @VICE @jmsbconcordia) he/him

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fe24da3221b06&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fthe-wild-world-of-crossword-data-71d560e222f5&user=Kurt+Reckziegel&userId=e24da3221b06&source=post_page-e24da3221b06--post_author_info--71d560e222f5---------------------follow_profile-----------)[Help](https://help.medium.com/hc/en-us?source=post_page-----71d560e222f5--------------------------------)[Status](https://medium.statuspage.io/?source=post_page-----71d560e222f5--------------------------------)[About](https://medium.com/about?autoplay=1&source=post_page-----71d560e222f5--------------------------------)[Careers](https://medium.com/jobs-at-medium/work-at-medium-959d1a85284e?source=post_page-----71d560e222f5--------------------------------)[Press](pressinquiries@medium.com?source=post_page-----71d560e222f5--------------------------------)[Blog](https://blog.medium.com/?source=post_page-----71d560e222f5--------------------------------)[Privacy](https://policy.medium.com/medium-privacy-policy-f03bf92035c9?source=post_page-----71d560e222f5--------------------------------)[Terms](https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----71d560e222f5--------------------------------)[Text to speech](https://speechify.com/medium?source=post_page-----71d560e222f5--------------------------------)[Teams](https://medium.com/business?source=post_page-----71d560e222f5--------------------------------)




























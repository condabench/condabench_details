 A data\-driven look at marble racing \| Dr. Randal S. Olson      Dr. Randal S. Olson    [**Dr. Randal S. Olson**](https://randalolson.com/)        [HOME](https://randalolson.com/) [ABOUT](https://randalolson.com/#about) [CONTACT](https://randalolson.com/#contact) [BLOG](https://randalolson.com/blog) [RESUME](https://randalolson.com/resume) [CONSULTING](https://randalolson.com/consulting) MORE  [Publications](https://scholar.google.com/citations?user=LU96GEAAAAAJ)   [Code](https://github.com/rhiever)   [Mentoring](https://randalolson.com/mentoring)   [Teaching](https://randalolson.com/teaching)    [A data\-driven look at marble racing
====================================](/2020/05/24/a-data-driven-look-at-marble-racing/)

---

Published on **May 24, 2020** by [**Dr. Randal S. Olson**](/#about) 

  data analysis data visualization marble racing

  **10 min** READ

  
Race tracks. High stakes. Rabid fans. Marbles...?

Marble racing has taken the world by storm in 2020\. Unless you've been living under a rock \-\- which is entirely understandable given the state of the world \-\- you've probably seen marble racing in one form or another in the past few months. If not, you owe it to yourself to watch one of the most satisfying comeback stories of the year:


> Race [pic.twitter.com/POe5ujIQ5a](https://t.co/POe5ujIQ5a)
> 
> — viral posts (@BestViralPosts) [January 29, 2020](https://twitter.com/BestViralPosts/status/1222648826303066113?ref_src=twsrc%5Etfw)

[Jelle's Marble Runs](https://www.youtube.com/channel/UCYJdpnjuSWVOLgGT9fIzL0g) started as a quirky YouTube channel back in 2006 and has refined the art of marble racing to the point that many \-\-\- including sponsor [John Oliver](https://www.youtube.com/watch?v=z4gBMw64aqk) from Last Week Tonight \-\-\- consider marble racing a legitimate contender for the national sports spotlight. Given that Jelle's Marble Runs just completed their popular Marbula One competition last month, I was curious to look at the race results to see if these races were anything more than chaos.

Do some marbles race better than others? Who would I put my money on in season 2 of Marbula One? *Is one of the marbles having an affair?* If any of these questions interest you, read on and I'll answer some of them.

The first step to answering these questions was to get some data. Thankfully, all of the Marbula One videos are organized in a YouTube playlist available [here](https://www.youtube.com/playlist?list=PLSmWeUDtr9fBm-OMFrcYtDRnmPwvjKt_s). From every race, my marble racing analytics team recorded each marble racer's qualifier performance, total race time, average lap time, final rank, and some other statistics. That dataset is available for download on my website [here](/assets/2020/05/Jelles-Marble-Racing-Marbula-One.csv).

Do some marbles race better than others?
----------------------------------------

At first thought, it might seem like a ridiculous question to ask whether one marble racer is more skilled than another. All marbles are created equal, after all, and there's not much to differentiate one marble from another. However, it's clear that not all marbles trained equally in preparation for the first season of Marbula One. The chart below shows the distribution and median of race times of every individual marble racer, sorted from fastest to slowest race times.

Note that I had to standardize their race times because each of the race tracks took a varying amount of time. Thus, a marble's performance in one race is measured as how much faster or slower they were than the average time it took all of the marbles to complete that race track.

![Individual marble racer performance in Marbula One](opensource/tidytuesday/2020-06-02/images/0.png)[Starry](https://jellesmarbleruns.fandom.com/wiki/Starry) clocked in the greatest individual race time this Marbula One season, crossing the finish line a full 7 seconds faster than the bulk of the pack in the first race of the season. Unfortunately for [Team Galactic](https://jellesmarbleruns.fandom.com/wiki/Team_Galactic), Starry appeared to be fatigued after this race as she turned in mediocre performances for the rest of the season.

Outlier performances aside, we see something that's rather surprising in this data: **Several marbles seemed to consistently perform above average in season 1 of Marbula One**. [Snowy](https://jellesmarbleruns.fandom.com/wiki/Snowy), [Smoggy](https://jellesmarbleruns.fandom.com/wiki/Smoggy), [Speedy](https://jellesmarbleruns.fandom.com/wiki/Speedy), and [Prim](https://jellesmarbleruns.fandom.com/wiki/Prim) stand out as the top racers, consistently vying for the top spot in every race. Speedy especially demonstrated why he's considered one of the sport's top athletes with stellar performances in every Marbula One race.

On the other end of the spectrum \-\-\- and equally surprising \-\-\- we see that **some marbles consistently perform worse than their competitors**. [Mary](https://jellesmarbleruns.fandom.com/wiki/Mary), [Sublime](https://jellesmarbleruns.fandom.com/wiki/Sublime), [Vespa](https://jellesmarbleruns.fandom.com/wiki/Vespa), [Snowflake](https://jellesmarbleruns.fandom.com/wiki/Snowflake) somehow always found themselves behind everyone else, with Mary even failing to finish one race because she [fell a full lap behind](https://www.youtube.com/watch?v=QSNt3hW6f7g).

Let's look into how these performances affected their teams.

What marble teams should I bet on?
----------------------------------

If you're new to marble racing and looking for a took to root for, I've compiled a chart with you in mind. Below I show the distribution of each team's placement in every Marbula One race, sorted from the best\-ranking teams to the worst. If you like to root for the winners, pick a team near the top of this chart. If you like to root for the underdogs, pick a team near the bottom of this chart.

![Marble team performance in Marbula One](opensource/tidytuesday/2020-06-02/images/1.png)The [Savage Speeders](https://jellesmarbleruns.fandom.com/wiki/Savage_Speeders), one of the most decorated teams in Marble League history, lived up to their name this season and consistently ranked in the top 8\. The lone exception for the Savage Speeders was one out\-of\-character performance in race 5 from [Rapidly](https://jellesmarbleruns.fandom.com/wiki/Rapidly), where some suspect he put in a late night at the clubs the night before the race. The Savage Speeders will no doubt ride on this victory into the [2020 Marble League](https://jellesmarbleruns.fandom.com/wiki/Marble_League_2020) this summer, as they expect to easily pass the qualifiers and add to their mountain of gold medals.

The [Hornets](https://jellesmarbleruns.fandom.com/wiki/Hornets), on the other hand, are performing about as well as the NBA team they share a name with. As a relatively new team to the Marble League, the Hornets are still trying to make a name for themselves as they hope to avoid relegation. Luckily for them, the Hornets were officially invited to participate in this year's Marble League and will have the opportunity to prove that they belong in the big leagues.

Interestingly, teams such as the [Snowballs](https://jellesmarbleruns.fandom.com/wiki/Snowballs) and [Team Primary](https://jellesmarbleruns.fandom.com/wiki/Team_Primary) had an up\-and\-down Marbula One season, sometimes placing first in one race then placing last in the next \-\-\- much to the disappointment of their fans. Let's see why these teams seemed to struggle.

Some marble racing teams need a reshuffle
-----------------------------------------

To get a better idea of why some teams were so hot and cold during throughout the Marbula One season, I matched each team up on the line plot below. Each team had two athletes competing in this season, and I compared the average race rank of each team's athletes. As an example for team Snowballs, [Snowy](https://jellesmarbleruns.fandom.com/wiki/Snowy) ranked 3rd in every Marbula One race on average vs. [Snowflake](https://jellesmarbleruns.fandom.com/wiki/Snowflake)'s average rank of 13\.

![Mismatched teammates in Marbula One](opensource/tidytuesday/2020-06-02/images/2.png)From the above chart, it's clear that some teammates are holding their team back. Team Snowballs and Team Primary could have been in contention for the podium if it weren't for Snowflake and Mary, and [Sublime](https://jellesmarbleruns.fandom.com/wiki/Sublime) embarrassed his team in every race he participated in \-\-\- including a race he didn't even finish. What's worse is that Snowflake, Mary, and Sublime are all team captains, who you expect to lift their team up instead of hold them back.

It might be time for Snowflake and Mary to consider stepping back into managerial roles. It's been years since either of them have stood on the podium for individual events, and it's hard to deny that their recent performances are holding their teams back.

Does qualifier performance matter?
----------------------------------

The last question I wanted to investigate was brought to me by a [fellow marble racing fan](https://twitter.com/mepgg/status/1263283693596151808): Does qualifier performance matter? In Marbula One races, before the main race every marble completes one lap around the race track. Their performance in that one lap determines their starting position in the upcoming race, where the marble racer with the fastest qualifier lap starts ahead of everyone else and the marble racer with the slowest qualifier lap starts behind everyone else. Is a marble racer's fate sealed if they don't perform well in the qualifier?

To answer this question, I matched up each marble racer's qualifier rank (x\-axis) with their final rank in the corresponding race (y\-axis). To make the trend a little clearer, I binned the ranks into the Top 4, Ranks 5 \- 8, Ranks 9 \- 12, and the Bottom 4\.

![Comparison of qualifier rank vs. final race rank](opensource/tidytuesday/2020-06-02/images/3.png)In general, if a marble racer places in the top 50% in the qualifier, she will place in the top 50% in the race as well. The opposite case is true as well when a marble racer places in the bottom 50% of the qualifier. It's safe to say that **qualifiers generally decide who will [bring home points](https://jellesmarbleruns.fandom.com/wiki/Marbula_One) for their team in the upcoming race**.

However, **it's not unheard of for marble racers to defy the odds**. Snowy amazingly [claimed the gold](https://www.youtube.com/watch?v=3JJWQbWFxHc) in race 6 despite a poor showing in the qualifier, and Wospy infamously [failed to even complete race 2](https://www.youtube.com/watch?v=KTXbB0BVLZc) after an impressive showing in the qualifier. No matter the cause, fans live for these kinds of upsets!

The near future of marble racing
--------------------------------

In this post, I was quite surprised to discover that not all marble athletes are created equal, and that some marbles seem to consistently perform better or worse than their peers. It's possible that this is all statistical noise, but we'll have to wait for Marbula One season 2 sometime in [Autumn 2020](https://twitter.com/Jellesmarbles/status/1246922544864780291) to find out. Given the track record of some of these marble athletes, I suspect they will once again find themselves ahead of the pack in season 2\.

If you're excited for more marble racing, thankfully you won't have to wait very long. This year's Marble League starting in late June:

and there are plenty more events to catch up with on their YouTube [here](https://www.youtube.com/channel/UCYJdpnjuSWVOLgGT9fIzL0g/playlists). Enjoy, marble racers!

  BACK TO TOP   [##### Dr. Randal S. Olson

Full stack data scientist and artificial intelligence researcher](https://randalolson.com/#about)### More Links

- [RO Consulting](https://randalolson.com/consulting)
- [Mentoring](https://randalolson.com/mentoring)
- [Teaching](https://randalolson.com/teaching)
- [Subscribe via RSS](https://randalolson.com/feed.xml)
### Recent Posts

- [How to beat the Original I.Q. Tester](https://randalolson.com/2024/03/26/how-to-beat-original-iq-tester/)
- [Things I can lift: How I visualize my strength training progress](https://randalolson.com/2021/04/15/things-i-can-lift-week7/)
- [A data\-driven look at marble racing](https://randalolson.com/2020/05/24/a-data-driven-look-at-marble-racing/)
  2024 \| [WhatATheme](https://github.com/thedevslot/WhatATheme) \- A Theme made with  by [TheDevsLot](https://www.twitter.com/thedevslot) Powered by [Jekyll](https://jekyllrb.com/)

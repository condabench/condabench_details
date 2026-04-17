



A Statistical Curiosity Voyage Through the Emotion of Stranger Things








































































 Search
 





Submit your search query










[Forum](https://forum.freecodecamp.org/)
[Donate](https://www.freecodecamp.org/donate/)








ADVERTISEMENT







 November 6, 2017
 
/
[\#Data Science](/news/tag/data-science/) 

A Statistical Curiosity Voyage Through the Emotion of Stranger Things
=====================================================================













By Jordan Dworkin


Like [a few million](https://www.theringer.com/2017/11/2/16600190/stranger-things-season-2-ratings) other people, I spent the weekend of Oct. 27, 2017, watching Stranger Things 2, and the following week dealing with minor [withdrawal](https://twitter.com/search?f=tweets&vertical=default&q=stranger%20things%20withdrawal&src=typd).


To cope, and to transition back into my research, I decided to apply the statistical [paddles](https://i.pinimg.com/originals/3f/38/e3/3f38e374b22804b066db9b05e2ca15b8.jpg) of sentiment analysis and network analysis to the scripts from Seasons 1 and 2, and to consider what the results might say about the emotional structure of each episode of the show.


To begin understanding the emotion of Stranger Things, I downloaded the [scripts](https://www.springfieldspringfield.co.uk/episode_scripts.php?tv-show=stranger-things-2016) and assigned a numeric value to each word based on its [positive or negative valence](http://www2.imm.dtu.dk/pubdb/views/publication_details.php?id=6010). The simplest aspect of emotion to look at is the average valence of each episode. This metric is obtained by taking the mean sentiment value of all words in an episode, regardless of the order in which they are spoken.


![Image](opensource/tidytuesday/2022-10-18/images/0.png)


These values are generally what you might expect from a show about missing children and inter\-dimensional monsters, with most episodes showing more negative than positive emotion.


The most interesting finding seems to be the degree to which the [less\-than\-well\-received](https://www.vanityfair.com/hollywood/2017/10/stranger-things-recap-season-2-episode-7-eleven-mother-chicago-kali-millie-bobby-brown) Chicago episode — number 15 — stands out as being more than twice as negative as any other. This may be due to a combination of its dark plot and the lack of any comedic relief from the Hawkins gang.


However, there is a lot of temporal information missing from those averages, so let’s take a look at how the emotional tone changes over time within episodes.


One way to do this is to use the sliding window technique. For this version of a sliding window, we’re going to take the average of the 40 words surrounding a central word, then continually shift one word over and take a new average. This yields a smooth trajectory of the emotional valence over the course of each episode.


![Image](opensource/tidytuesday/2022-10-18/images/1.png)


While it’s difficult to learn much from simply looking at the trajectories, a few things do pop out.


First, with only one exception (you guessed it, the Chicago episode), even the darkest episodes typically have a few scenes that are heavy on positive sentiment.


Second, of the 17 episodes, only three end on a high note: the Season 1 finale, the Season 2 premiere, and the Season 2 finale.


Third, there is a lot of variation in how these episodes are structured, and they don’t seem to follow a clear emotional pattern. Let’s roll with that last point and see if we can characterize some of that variation.


As a baseline for comparison, we can check whether the season in which an episode appears contains enough information to explain similarities and differences across emotional trajectories.


![Image](opensource/tidytuesday/2022-10-18/images/2.png)


Unsurprisingly, it does not `(_p_ = .34)`. In general, both Season 1 and Season 2 have a great deal of variability in their episodes’ structures. The average trajectories both tend to hover around neutral.


To find a better classification, let’s first conceptualize the relationships between episodes as a network by calculating the temporal correlation for every pair of episodes. In this context, the nodes are episodes and the edges represent the degree to which pairs show similar patterns of emotion.


Once this network is constructed, we can apply [methods](https://perso.uclouvain.be/vincent.blondel/research/louvain.html) borrowed from [graph theory](https://en.wikipedia.org/wiki/Graph_theory) to find communities in our data. In this case, three distinct episode groups are revealed, and the within\-group similarity is greater than would be expected to occur by chance `(_p_ < .0`01\).


Now that we’ve found our communities of interest, let’s map them back onto the emotion trajectories to see if they capture any more of the variability.


![Image](opensource/tidytuesday/2022-10-18/images/3.png)


Unlike the division by season, these average group trajectories appear to describe three distinct patterns. They also seem to track fairly well onto their underlying episode trajectories.


Looking at the average patterns, we can see that group 1 contains episodes that begin and end with neutral emotion and have slow fluctuations in the middle, group 2 contains episodes that begin with negative emotion and gradually climb towards a positive ending, and group 3 contains episodes that begin on a positive note and oscillate downwards towards a darker ending.


In addition to plotting the communities of emotion patterns, let’s take a look at the full network structure.


![Image](opensource/tidytuesday/2022-10-18/images/4.png)


The first thing that jumps out is that each group contains an approximately equal number of episodes from Season 1 and Season 2\. This supports the earlier finding that season is not a good predictor of episode similarity. We can also see that episode 15 again stands out from the rest. This time because it is more loosely connected to the rest of the graph than any of the other episodes.


Perhaps most interestingly, the network reveals that episodes tend to be less like those preceding and proceeding them than you would expect to occur by chance`(_p_ = .03)`. Additionally, the transitions from episodes 1→2, 2→3, and 3→4 have three of the five largest shifts in emotional structure of the 16 transitions that occurred in the show.


Together, these results suggest that varying the emotional trajectory from episode to episode may be a strategy for [getting viewers hooked](https://www.vanityfair.com/hollywood/2016/09/netflix-episode-that-got-you-hooked).


Will future episodes continue to show these changes in emotional structure? Will they follow the same three dominant emotional trajectories? Will future attempts at creating boldly different episodes land better than Chicago? Chalk those up as more [unanswered questions](https://www.theringer.com/tv/2017/11/6/16604702/stranger-things-season-3-questions) for Season 3\.


***Miscellaneous observations \[some spoilers ahead]***


* Series emotional high point: Christmas at the Byers household in the Season 1 finale.



```
What are you - What are you doing? [Jonathan] Documenting.Oh, why? - Because - [Joyce chuckles] - It looks great. - [Joyce] Oh, this is just so overcooked. - And look, the potatoes are runny.- [Jonathan] Mom. - [Joyce] They're so runny.- [Jonathan chuckles] Mom, it's gonna be great.

```
* Series emotional low point \#1: Chase scene to open Season 2\.



```
[Horns honking] Shit! Shit! Shit! Shit! Shit! [Cackles] [Exhales] Okay. Okay.[Police sirens wailing] - Son of a bitch! We got more! - [Mick] Oh, shit! They're headed down 7th.

```
* Series emotional low point \#2: Steve vs. Billy in the Season 2 finale.



```
[Steve] Get out.[Dustin] Yes! Kick his ass, Steve! - [Mike] Get him! - [Dustin] Murder the son of a bitch! - [Dustin] Now! Now! - [Mike] Get that shithead! - [Dustin] Kill the son of a bitch! - [Lucas] Steve! - [Max] Billy! - [Mike] Holy shit! Shit!

```
* Honorable mention for the best scene that could not be counted because of the lack of dialogue: Billy in the mirror.



```
[Billy preens]

```
For those interested, code for this project is publicly available [here](https://www.dropbox.com/s/6hvtd9m8d9dvl86/EmotionOfStrangerThings.R?dl=0).









---



 If you read this far, thank the author to show them you care. Say Thanks






 Learn to code for free. freeCodeCamp's open source curriculum has helped more than 40,000 people get jobs as developers. [Get started](https://www.freecodecamp.org/learn/)






ADVERTISEMENT









freeCodeCamp is a donor\-supported tax\-exempt 501(c)(3\) charity organization (United States Federal Tax Identification Number: 82\-0779546\)


Our mission: to help people learn to code for free. We accomplish this by creating thousands of videos, articles, and interactive coding lessons \- all freely available to the public.


Donations to freeCodeCamp go toward our education initiatives, and help pay for servers, services, and staff.



 You can [make a tax\-deductible donation here](https://www.freecodecamp.org/donate/).
 




Trending Books and Handbooks
----------------------------


* [Learn CSS Transform](https://www.freecodecamp.org/news/complete-guide-to-css-transform-functions-and-properties/)
* [Build a Static Blog](https://www.freecodecamp.org/news/how-to-create-a-static-blog-with-lume/)
* [Build an AI Chatbot](https://www.freecodecamp.org/news/how-to-build-an-ai-chatbot-with-redis-python-and-gpt/)
* [What is Programming?](https://www.freecodecamp.org/news/what-is-programming-tutorial-for-beginners/)
* [Python Code Examples](https://www.freecodecamp.org/news/python-code-examples-sample-script-coding-tutorial-for-beginners/)
* [Open Source for Devs](https://www.freecodecamp.org/news/a-practical-guide-to-start-opensource-contributions/)
* [HTTP Networking in JS](https://www.freecodecamp.org/news/http-full-course/)
* [Write React Unit Tests](https://www.freecodecamp.org/news/how-to-write-unit-tests-in-react-redux/)
* [Learn Algorithms in JS](https://www.freecodecamp.org/news/introduction-to-algorithms-with-javascript-examples/)
* [How to Write Clean Code](https://www.freecodecamp.org/news/how-to-write-clean-code/)
* [Learn PHP](https://www.freecodecamp.org/news/the-php-handbook/)
* [Learn Java](https://www.freecodecamp.org/news/the-java-handbook/)
* [Learn Swift](https://www.freecodecamp.org/news/the-swift-handbook/)
* [Learn Golang](https://www.freecodecamp.org/news/learn-golang-handbook/)
* [Learn Node.js](https://www.freecodecamp.org/news/get-started-with-nodejs/)
* [Learn CSS Grid](https://www.freecodecamp.org/news/complete-guide-to-css-grid/)
* [Learn Solidity](https://www.freecodecamp.org/news/learn-solidity-handbook/)
* [Learn Express.js](https://www.freecodecamp.org/news/the-express-handbook/)
* [Learn JS Modules](https://www.freecodecamp.org/news/javascript-es-modules-and-module-bundlers/)
* [Learn Apache Kafka](https://www.freecodecamp.org/news/apache-kafka-handbook/)
* [REST API Best Practices](https://www.freecodecamp.org/news/rest-api-design-best-practices-build-a-rest-api/)
* [Front\-End JS Development](https://www.freecodecamp.org/news/front-end-javascript-development-react-angular-vue-compared/)
* [Learn to Build REST APIs](https://www.freecodecamp.org/news/build-consume-and-document-a-rest-api/)
* [Intermediate TS and React](https://www.freecodecamp.org/news/build-strongly-typed-polymorphic-components-with-react-and-typescript/)
* [Command Line for Beginners](https://www.freecodecamp.org/news/command-line-for-beginners/)
* [Intro to Operating Systems](https://www.freecodecamp.org/news/an-introduction-to-operating-systems/)
* [Learn to Build GraphQL APIs](https://www.freecodecamp.org/news/building-consuming-and-documenting-a-graphql-api/)
* [OSS Security Best Practices](https://www.freecodecamp.org/news/oss-security-best-practices/)
* [Distributed Systems Patterns](https://www.freecodecamp.org/news/design-patterns-for-distributed-systems/)
* [Software Architecture Patterns](https://www.freecodecamp.org/news/an-introduction-to-software-architecture-patterns/)




Mobile App
----------



* 
* 







Our Charity
-----------



[About](https://www.freecodecamp.org/news/about/) 
[Alumni Network](https://www.linkedin.com/school/free-code-camp/people/) 
[Open Source](https://github.com/freeCodeCamp/) 
[Shop](https://www.freecodecamp.org/news/shop/) 
[Support](https://www.freecodecamp.org/news/support/) 
[Sponsors](https://www.freecodecamp.org/news/sponsors/) 
[Academic Honesty](https://www.freecodecamp.org/news/academic-honesty-policy/) 
[Code of Conduct](https://www.freecodecamp.org/news/code-of-conduct/) 
[Privacy Policy](https://www.freecodecamp.org/news/privacy-policy/) 
[Terms of Service](https://www.freecodecamp.org/news/terms-of-service/) 
[Copyright Policy](https://www.freecodecamp.org/news/copyright-policy/) 








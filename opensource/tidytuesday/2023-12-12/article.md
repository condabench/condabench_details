








Christmas Movies \| Department of Network and Data Science























[Skip to main content](#main-content)


* [CEU Home](https://www.ceu.edu)
* [Intranet](https://ceuedu.sharepoint.com/sites/MyCEU)
* [Give](https://giving.ceu.edu)
* [Shop](https://shop.ceu.edu)
* [Apply](https://www.ceu.edu/admissions/how-to-apply/checklist)
* [Alumni](https://alumni.ceu.edu)
* [Careers](https://careers.ceu.edu/?utm_source=corporatesite)
* [CEU PU \- Deutsch](https://www.ceu.edu/node/25238)
* [Közép\-európai Egyetem](https://www.ceu.edu/hu/kee/about)




 


[Department of Network  
and Data Science](/ "Home")


* [Programs](/programs)
	+ [BA/BSc in Data Science and Society](/bachelor-arts-bachelor-science-data-science-and-society)
	+ [MSc in Social Data Science](/msc-social-data-science)
	+ [PhD in Network Science](/phd-program-network-science)
	+ [Advanced Certificate Programs](/advanced-certificate-programs)
	+ [Doctoral Research Support](/doctoral-research-support)
	+ [Course Registration](/course-registration)
	+ [Schedules](/schedules)
	+ [Brochure](/brochure)
* [People](/people)
	+ [Faculty](/faculty)
	+ [Visiting Faculty](/visiting-faculty)
	+ [Research Fellows](/research-fellows)
	+ [PhD Students \& Alumni](/phd-students-alumni)
	+ [Former Visitors](/former-visitors)
	+ [Staff](/staff)
* [Research](/research)
* [Events](https://events.ceu.edu/host/department-network-and-data-science)
* [What's Up at DNDS](/blogs)
* SearchSearchSearch

 

* [Log in](/user/login)

 


Toggle navigation












 



1. [Home](/)
2. [News](/news)
3. Christmas Movies

 
Christmas Movies
================












 December 16, 2019 



As the holiday season is approaching, also reflected in Google Trends (Figure 1\), probably many of us are preparing to enjoy some recreational movie nights – but where to start? Here I analyze movies from the Internet Movie Database (IMDb \[1]) that users related to Christmas.




![](opensource/tidytuesday/2023-12-12/images/0.png)  

Figure 1: The popularity of the keyword Christmas in Google search results (Source: [www.google.com/trends](http://www.google.com/trends) [https://trends.google.com/trends/explore?geo\=US\&q\=Christmas](https://trends.google.com/trends/explore?geo=US&q=Christmas)).





For this, I collected all the movies from IMDb that contain the keyword *Christmas* added by the platform's users, and gained at least 10 votes since their release, comprising a dataset of 7,512 films.


First, I compared the movies based on their popularity (number of votes on IMDb) and listed the Top 20 in Figure 2\. The figure shows that the IMDb community certainly thinks “Die Hard” is a Christmas movie with its \~740k votes, while the old\-time classic “Home Alone” only catches the 5th position on the list. Surprisingly, none of the top three movies won an Oscar (although they were nominated). Out of the 20 movies, 11 were nominated for the prestigious award, and 4 won.




![](opensource/tidytuesday/2023-12-12/images/1.png)  

Figure 2: The Top 20 highest voted movies on IMDb tagged with the keyword Christmas. The colors encode whether a certain movie has won an Oscar, got nominated, or neither.





Next, I extracted the Top 5 keywords for each Christmas movie and constructed their co\-occurrence network (Figure 3\). The giant component consists of XXX keywords after applying a backbone filtering algorithm \[2], and lets us explore the typical topics centered by keywords such as the general themes of *Christmas Eve*, *Santa Claus*, and *winter*, or different sorts of transportation methods, like *reindeer* and *train.* Less expected topics emerged as well, like *talking animals* or *nudity*.




![](opensource/tidytuesday/2023-12-12/images/2.png)  

Figure 3: Keyword co\-occurrence network. Node size is proportional to the frequency (number of movies) each keyword was associated with, while the colors encode total popularity of the movies they occurred in.





Finally, I used these keywords to group the different movies together based on the number of keywords they shared. This resulted in a core network of 2,181 movies (Figure 4\), where the stronger the connection between the two movies is, the more similar they are. Consequently, the most central nodes in this network are the most general regarding their topics, the ones being the most alike to the rest of their neighborhood. These most “general” movies are the largest nodes on the figure, and while some of them sound familiar (e.g. *Rocky*), most of them are quite unknown (e.g. *The Christmas Goose*) yet are promised to be a good mixture of Christmas\-related topics. Therefore, a good strategy to map out the Christmas movies landscape is to pick the largest nodes, evaluate their topics, and then go for some of their highly\-voted neighbors. Please find a searchable pdf movie\-map [here](https://networkdatascience.ceu.edu/sites/cns.ceu.edu/files/attachment/article/544/xmasmovies.pdf) (or see the file attached below the blog post; you can also click on Figure 4 to access it).




[![](opensource/tidytuesday/2023-12-12/images/3.png)](https://networkdatascience.ceu.edu/sites/cns.ceu.edu/files/attachment/article/544/xmasmovies.pdf)
Figure 4: Each node represents a Christmas movie, while the size of the nodes is proportional to how “general” the topic of a movie (set of keywords) is, while the color of the movies from red to green shows the increase in popularity.  






\[1] [www.imdb.com](http://www.imdb.com)


\[2] *Network backboning with noisy data*. Coscia, Michele and Neffke, Frank MH, 2017


Blog post by [Milán Janosov](/node/232)   



 



Attachment:  [Xmas movies map](https://networkdatascience.ceu.edu/sites/cns.ceu.edu/files/attachment/article/544/xmasmovies.pdf "xmasmovies.pdf") 











Category: [What's Up at DNDS](/blogs) 


Share
-----








 















apply
-----


* [Apply Now](https://www.ceu.edu/admissions/how-to-apply/checklist)
* [Sign up for more](https://ceu.my.salesforce-sites.com/inquiry/TargetX_Base__InquiryForm#?formId=a0AP8000000ngNuMAI&formType=general)




learn more
----------


* [Subscribe to newsletter](/subscribe-our-events-newsletter)




connect with us
---------------


* [facebook](https://www.facebook.com/DNDS.CEU/)
* [twitter](https://twitter.com/dnds_ceu)










**Copyright © Central European University**


[CEU Data Privacy Notice](http://www.ceu.edu/privacy) \| [Imprint/Impressum](https://www.ceu.edu/node/25986) \| [Accessibility at CEU](https://www.ceu.edu/accessibility-ceu)  
Postal Address Austria: Central European University Private University \| Quellenstraße 51 \| A\-1100 Wien, Austria \| Vienna Commercial Court \| FN 502313 x  
Postal Address Hungary: Közép\-európai Egyetem \| Nádor u. 9\. \| 1051 Budapest, Hungary













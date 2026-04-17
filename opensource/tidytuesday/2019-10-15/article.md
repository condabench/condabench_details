




Ellis Hughes · Ellis Hughes







[Ellis Hughes
============](/ "Ellis Hughes")
#### blogs and musings of a bioengineer turned data scientist








[Home](/)
[Archive](/post/)




[Big mtcars](/thebioengineer.github.io/2019/09/10/big-mtcars/)
==============================================================



 Tue, Sep 10, 2019 \- Read in 32 Min
 


 MTCARSLets admit it, the mtcars dataset is basically beat to death. Who hasn’t seen the example of regressing displacement vs mpg to show, surprise, there is a relationship. It seems like it has worked its way into every introductory R class known.
So, lets go bigger
Luckily for us, the kind folks over at the EPA have been hard at work reviewing how our cars are doing.
 [Read more...](/thebioengineer.github.io/2019/09/10/big-mtcars/)






[ifelse then if\_else](/thebioengineer.github.io/2019/09/05/ifelse-then-if-else/)
=================================================================================



 Thu, Sep 5, 2019 \- Read in 4 Min
 


 Problem StatementToday one of my colleagues posted a question into our R slack community asking why when she was using ifelse that her date field was being converted into a numeric.
date1\<\-as.Date(c("2019\-01\-01","2019\-01\-02","2019\-01\-03"))date2\<\-as.Date(c("2019\-01\-02","2018\-01\-02","2019\-01\-03"))ifelse(date1\>date2,date1,date2\)\#\# \[1] 17898 17898 17899My first instinct was that date objects (and POSIXct objects) are numeric objects that are counting the number of days or seconds since the origin (January 1, 1970 in R).
 [Read more...](/thebioengineer.github.io/2019/09/05/ifelse-then-if-else/)






[R in Pharma](/thebioengineer.github.io/2019/08/26/r-in-pharma/)
================================================================



 Mon, Aug 26, 2019 \- Read in 1 Min
 


 Below are the slides I presented at this years R/Pharma conference. It was a blast and I met so many great people. I learned about the many ways R is being used in the industry, and how there is a huge push towards collaboration and transparancy in sharing our code.
I discussed our approach to creating the documentaion required to validate an internally generated R package and lessons learned working in a group.
 [Read more...](/thebioengineer.github.io/2019/08/26/r-in-pharma/)






[Arcade Games using R and TensorFlow](/thebioengineer.github.io/2019/07/09/arcade-games-using-r-and-tensorflow/)
================================================================================================================



 Tue, Jul 9, 2019 \- Read in 11 Min
 


 Reinforcement learning is an interesting technique where in the user gives a model a game state and requests that it produce some sort of reaction to the state. This action is then fed back into the model to generate the next state. If the result of this action is a positive reaction, it is recorded and the model is fit to imply this action is a good one.
 [Read more...](/thebioengineer.github.io/2019/07/09/arcade-games-using-r-and-tensorflow/)




[Home](/)
[Archive](/post/)
[Top](#top)




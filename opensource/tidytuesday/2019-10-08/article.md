





Part I: Getting old? You can still lift! – Elias Oziolor, Ph.D.






























































































  









[Skip to content](#content)




* [GitHub](http://github.com/eoziolor)
 



 [Elias Oziolor, Ph.D.](https://oziolor.wordpress.com/)
======================================================


Evolutionary genomics in a toxic world
--------------------------------------






Primary Menu
* [About](https://oziolor.wordpress.com/about/)
* [Curriculum Vitae](https://oziolor.wordpress.com/curriculum-vitae/)
* [Science blogs](https://oziolor.wordpress.com/category/science-blogs/)
* [Publications](https://oziolor.wordpress.com/publications/)
* [Powerful data](https://oziolor.wordpress.com/category/powerful-data-posts/)
 

Search


Search for:



 









[Powerful data posts](https://oziolor.wordpress.com/category/powerful-data-posts/)Part I: Getting old? You can still lift!
========================================

 

**Powerful Data Project** Part I: Getting old? You can still lift!
==================================================================


Aging is normal. Unfortunately, it leaves some powerlifters discouraged about their abilities to still lift well and accomplish PRs when they get older. How important is your age when it comes to the amoutn of weight you lift? Should you start focusing more on endurance and give up on lifting good weights once you hit 40…50…60? Let’s take a stab at some of these questions and dig through a rather **powerful** dataset that has some pointers for us.


Image featured from Mark Bell’s Supertraining gym is Eddy Coan, one of the best powerlifters, still smashing super heavy weights in his mid\-50s!


The first thing that I will do is getting the data and all the necessary packages that I need from R to analyze it. And look at what I have.



```
## 'data.frame':    601229 obs. of  38 variables:
##  $ MeetID        : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ LifterID      : int  1 2 2 2 3 4 5 5 6 6 ...
##  $ Name          : chr  "Angie Belk Terry" "Dawn Bogart" "Dawn Bogart" "Dawn Bogart" ...
##  $ Sex           : chr  "F" "F" "F" "F" ...
##  $ Event         : chr  "SBD" "SBD" "SBD" "B" ...
##  $ Equipment     : chr  "Wraps" "Single-ply" "Single-ply" "Raw" ...
##  $ Age           : int  47 42 42 42 18 28 60 60 52 52 ...
##  $ Division      : chr  "Mst 45-49" "Mst 40-44" "Open Senior" "Open Senior" ...
##  $ BodyweightKg  : int  60 59 59 59 64 62 67 67 66 66 ...
##  $ WeightClassKg : chr  "60" "60" "60" "60" ...
##  $ Squat1Kg      : num  38.6 120.2 120.2 NA NA ...
##  $ Squat2Kg      : num  47.6 136.1 136.1 NA NA ...
##  $ Squat3Kg      : num  -54.4 142.9 142.9 NA NA ...
##  $ Squat4Kg      : num  NA NA NA NA NA ...
##  $ BestSquatKg   : num  47.6 142.9 142.9 NA NA ...
##  $ Bench1Kg      : num  15.9 88.5 88.5 88.5 29.5 ...
##  $ Bench2Kg      : num  20.4 95.2 95.2 95.2 31.8 ...
##  $ Bench3Kg      : num  -24.9 -97.5 -97.5 -97.5 -34 ...
##  $ Bench4Kg      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ BestBenchKg   : num  20.4 95.2 95.2 95.2 31.8 ...
##  $ Deadlift1Kg   : num  61.2 136.1 136.1 NA 90.7 ...
##  $ Deadlift2Kg   : num  70.3 149.7 149.7 NA -97.5 ...
##  $ Deadlift3Kg   : num  -77.1 163.3 163.3 NA NA ...
##  $ Deadlift4Kg   : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ BestDeadliftKg: num  70.3 163.3 163.3 NA 90.7 ...
##  $ TotalKg       : num  138.3 401.4 401.4 95.2 122.5 ...
##  $ Place         : chr  "1" "1" "1" "1" ...
##  $ Wilks         : num  155 456 456 108 130 ...
##  $ McCulloch     : num  168 466 466 110 138 ...
##  $ MeetPath      : chr  "365strong/1601" "365strong/1601" "365strong/1601" "365strong/1601" ...
##  $ Federation    : chr  "365Strong" "365Strong" "365Strong" "365Strong" ...
##  $ Date          : chr  "2016-10-29" "2016-10-29" "2016-10-29" "2016-10-29" ...
##  $ MeetCountry   : chr  "USA" "USA" "USA" "USA" ...
##  $ MeetState     : chr  "NC" "NC" "NC" "NC" ...
##  $ MeetTown      : chr  "Charlotte" "Charlotte" "Charlotte" "Charlotte" ...
##  $ MeetName      : chr  "Junior & Senior National Powerlifting Championships" "Junior & Senior National Powerlifting Championships" "Junior & Senior National Powerlifting Championships" "Junior & Senior National Powerlifting Championships" ...
##  $ Group         : chr  "45-49" "40-44" "40-44" "40-44" ...
##  $ GroupKG       : chr  "56-65" "56-65" "56-65" "56-65" ...

```

Obviously this is a fantastic and well kept dataset! **Great job** openpowerlifting.com!


I want to draw your attention that there are so many columns in this dataset, each containing unique information about each lifter. This will give us a lot of power to draw some observations about patterns of skills and potentials of the lifters. First I want to start by breaking them up into age ranges. I don’t like the ones drawn by more federations for my purposes. I want to have a bit higher resolution, so I will break them up into 5 year age gaps and see how things go from there.


I am also breaking them up into men and women for physiological reasons. I will be asking questions about max lift strength, so I don’t want to obscure the findings for either of those groups.


How much does age matter in the weight you lift?
------------------------------------------------


We can start gaining some initial insight by plotting relationships here. Let’s see for each lifter, what their total was and at what age they lifted it. When we plot these relationships over hundreds of thousands of people, this might clue us into some trends of how age affects your totals. I will start by plotting up the total lifts of men and women versus their age as a first pass. In addition, I will break these up into the equipment used to lift this weight (Multi\-ply, Raw, Single\-ply, Wraps) because that is likely a strong co\-variate (another variable that might also explain total weight lifted and obscure our relationships).


![1](data_artifacts/tidytuesday/2019-10-08/images/11.png)![2](data_artifacts/tidytuesday/2019-10-08/images/21.png)


 


There’s an obvious peak around age 25, with a slowdown afterwards. What does that mean? We have a ton of data and variability, let’s take a zoomed out view I’m plotting a distribution of data in different ages to see how representative we are and what the resolution. What you will see is that I grouped individual in age\-groups of 5 years. Then I plot the performance (total weight lifted) of those age groups in a distribution. This takes form as a “violin plot”. In each group you will see a blob that sort of looks like a violin. The locations on the y axis that the violin is “fatter” show that there is a large amount of lifters that represent that portion of the distribution. Where the violin is “skinnier”, then there are few lifters there.


![3](data_artifacts/tidytuesday/2019-10-08/images/3.png)![4](data_artifacts/tidytuesday/2019-10-08/images/4.png)


### What does this mean?


What you see on the x axis are the age groups that I added to the data earlier. The higher the plot, the stronger the lifters. The higher the horizontal line across the violins, the higher the median of that group is.


There is clear evidence of a pretty consistent relationship, showing both men and women peak overall in their mid\-20’s…How true is that though?


I ran a linear model, which is basically a fancy way to statistically look at a relationship between variables. In our case I want to know how much do **Age** and **Bodyweight** affect one’s total. This model asks this. If you see a positive number next to either Age or Bodyweight, that means that the older or heavier you are, the more you tend to lift as your TotalKg.



```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = men)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -752.39  -68.92    3.04   72.80  512.23 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          390.40274    3.05343  127.86   <2e-16 ***
## Age                   -1.19420    0.02499  -47.78   <2e-16 ***
## BodyweightKg           3.98592    0.01480  269.35   <2e-16 ***
## EquipmentRaw        -170.38049    2.60886  -65.31   <2e-16 ***
## EquipmentSingle-ply  -77.40003    2.61819  -29.56   <2e-16 ***
## EquipmentWraps      -133.16085    2.67832  -49.72   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 111.6 on 133743 degrees of freedom
##   (885 observations deleted due to missingness)
## Multiple R-squared:  0.4118, Adjusted R-squared:  0.4118 
## F-statistic: 1.873e+04 on 5 and 133743 DF,  p-value: < 2.2e-16

```


```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = women)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -326.76  -46.84   -2.48   44.63  344.43 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          305.10687    4.21639   72.36   <2e-16 ***
## Age                   -0.41827    0.02673  -15.64   <2e-16 ***
## BodyweightKg           2.12087    0.01844  115.03   <2e-16 ***
## EquipmentRaw        -134.68305    3.93889  -34.19   <2e-16 ***
## EquipmentSingle-ply  -44.54240    3.95998  -11.25   <2e-16 ***
## EquipmentWraps      -117.08138    4.01126  -29.19   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 72.4 on 56733 degrees of freedom
##   (216 observations deleted due to missingness)
## Multiple R-squared:  0.3358, Adjusted R-squared:  0.3358 
## F-statistic:  5737 on 5 and 56733 DF,  p-value: < 2.2e-16

```

The important things from what you see above are in two columns: 1\) Under coefficients: “Estimate” and “Pr(\>\|t\|)”. The estimate column can be read as such: “When you increase the parameter (in this case Age or Bodyweight) by one unit, your TotalKg changes by this much.” This is **cool**! It’s way cool because even though the relationship between Age and Total weight lifted is significantly negative (the Pr column has a very small number), in both men and women, this relationship is not very strong. On average men lose about 1\.2kg of their total per year of aging, while women lose about .5\.


The **much stronger** relationship is between bodyweight ant Total. Men gain almost 4kg for each 1kg in bodyweight and for women that relationship is more like 2:1\.


So maybe age is not that huge of a predictor of your lifting potential. This analysis has a flaw. I am considering all men and all women competing overall. What this doesn’t grasp is the fact that we have a sort of curve in the middle, where people in their mid 20’s peak. Let’s dive in.


I’m going to cull the data to remove people under 24\. In the time before 25, the total actually increases with age and it creates a weird hump that may be obscuring some patterns.


I’ll check what the patterns are for younger people later on!


![5](data_artifacts/tidytuesday/2019-10-08/images/5.png)![6](data_artifacts/tidytuesday/2019-10-08/images/6.png)


Now the negative relationships with age are starting to become more and more obvious. Let’s take a look with our fancy *linear model* again. This time, we have excluded the younger people and we can purely look at the decline of strenght, past the peak in mid\-20s.



```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = men2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -757.61  -65.80    1.75   67.91  468.77 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          572.95247    3.56795  160.58   <2e-16 ***
## Age                   -4.28207    0.03359 -127.48   <2e-16 ***
## BodyweightKg           3.48279    0.01817  191.72   <2e-16 ***
## EquipmentRaw        -180.19525    2.72644  -66.09   <2e-16 ***
## EquipmentSingle-ply  -67.47764    2.73648  -24.66   <2e-16 ***
## EquipmentWraps      -141.44523    2.81157  -50.31   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 104.4 on 75922 degrees of freedom
##   (606 observations deleted due to missingness)
## Multiple R-squared:  0.4802, Adjusted R-squared:  0.4802 
## F-statistic: 1.403e+04 on 5 and 75922 DF,  p-value: < 2.2e-16

```


```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = women2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -301.14  -46.28   -3.64   41.78  328.78 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          409.88862    4.79269   85.52   <2e-16 ***
## Age                   -2.21699    0.03891  -56.98   <2e-16 ***
## BodyweightKg           1.85859    0.02277   81.63   <2e-16 ***
## EquipmentRaw        -151.43106    4.25818  -35.56   <2e-16 ***
## EquipmentSingle-ply  -47.64090    4.29682  -11.09   <2e-16 ***
## EquipmentWraps      -134.20279    4.34645  -30.88   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 70.47 on 33965 degrees of freedom
##   (153 observations deleted due to missingness)
## Multiple R-squared:  0.376,  Adjusted R-squared:  0.3759 
## F-statistic:  4093 on 5 and 33965 DF,  p-value: < 2.2e-16

```

### Age is starting to matter a little more


The relationship between Age and TotalKg is larger now. That’s because we are looking after this original growth period now. Men seem to be losing closer to 4\.2kg per year off their total, while women lose about 2\.2kg. Good for women! One interpretation is that as you get older, it’s more difficult to lift heavy weights…duh. Obviously we have a bodyweight disparity here too, where the bigger you are, the more you will lift. An interesting interaction here suggests though, that there is a negative correlation between age and bodyweight, meaning: the older you are, you lose bang for the buck in bodyweight – is this real?


So far we have been looking at this accross all equipment types, let’s break it down and see if these relationships hold among all. What I’m doing here is grabbing the data and splitting it between equipment types. Then I’ll look at the relationship betwee Age and Total weight lifted, as well as the one between Bodyweight and Total weight lifted. This will yield a similar linear model as above, but for much more specific groups now.



```
##  (Intercept)          Age BodyweightKg 
##   596.328109    -5.410918     3.687664

```


```
##  (Intercept)          Age BodyweightKg 
##   406.302588    -3.593935     3.076590

```


```
##  (Intercept)          Age BodyweightKg 
##   490.196102    -4.920829     3.928118

```


```
##  (Intercept)          Age BodyweightKg 
##   443.402471    -4.223248     3.344580

```


```
##  (Intercept)          Age BodyweightKg 
##   329.775536    -1.233394     2.425924

```


```
##  (Intercept)          Age BodyweightKg 
##   270.472244    -1.781078     1.463824

```


```
##  (Intercept)          Age BodyweightKg 
##   337.283066    -3.328599     2.894045

```


```
##  (Intercept)          Age BodyweightKg 
##   268.636496    -1.665245     1.681378

```

So this is **REALLY** interesting! Let’s break down these results:  

What you see here is that different equipment types have a difference in how Age and Bodyweight affect the Totals:


* Men
	+ Multi\-ply – **large** loss of total with Age, **decent** gain of Total with Bodyweight
	+ Raw – **decent** loss of total with Age, **decent** gain of Total with Bodyweight
	+ Single\-ply – **large** loss of total with Age, **decent** gain of Total with Bodyweight
	+ Wraps – **large** loss of total with Age, **decent** gain of Total with Bodyweight
* Women
	+ Multi\-ply – **small** loss of total with Age, **decent** gain of Total with Bodyweight
	+ Raw – **small** loss of total with Age, **small** gain of Total with Bodyweight
	+ Single\-ply – **decent** loss of total with Age, **decent** gain of Total with Bodyweight
	+ Wraps – *\_\_very small*\_ loss of total with Age, **small** gain of Total with Bodyweight


Now this is super interesting. Is this a real relationship or do we maybe just have a lack of representation of older or bigger lifters in some leagues?


![7](data_artifacts/tidytuesday/2019-10-08/images/7.png)![8](data_artifacts/tidytuesday/2019-10-08/images/8.png)  

When we look at Age in each league, we do see that there are proportionally slightly more older lifters in the Multy\-ply and Single\-ply categories. What you see is that the violin plot above looks a little thicker at the higher age ranges (y axis). This suggests to us that proportionally, those Eqiupment types attract a little more lifters than they do in the Raw class/or Wraps. This could be because Raw and Wraps are also much more popular with the new generation of lifters, while the other two classes are much more historically prevelant, especially in the United States. You can see the over\-representation of young Raw and Wraps lifters by the thickness of the violin plot at the bottom of the y axis.


Now let’s see what the distribution of weights looks like among equipment types to see if we see as trend amongst them.


![9](data_artifacts/tidytuesday/2019-10-08/images/9.png)![10](data_artifacts/tidytuesday/2019-10-08/images/10.png)  

There is a strange trend to have heavier lifters in the Multi\-ply and Wraps divisions for men. This could be a difference in the weight categories offered by different leagues that support multi\-ply, vs ones that don’t.


In women, we do see smaller lifters in the Single\-ply category, but other than that things seem pretty equal in terms of distrubtion. Remember the wider the violin, the more lifters are there.


You can see clearly the categories by the wiggle in distribution, each wiggle is a high proportion of people likely at the top of their weight class, where there are less lifters at the bottom of a weight class.


Now that doesn’t tell us too much about how these are distributed over age, but these are interesting trends to look at anyways! What I’d like to see is if we see a relationship between the bodyweight of lifters and their age. Let’s plot that up.


![11](data_artifacts/tidytuesday/2019-10-08/images/111.png)![12](data_artifacts/tidytuesday/2019-10-08/images/12.png)


Something smells fishy here though! (and no it’s not the knee sleeves I haven’t washed in 3 months)


We saw that both Age and Weight have some effect on the weight lifted by people, but do we just see a large proportion of monster heavyweight lifters in the younger categories? The strange thing we are seeing here is that there seems to be a cap on older lifters in both men and women, where the older you get the less lifters in heavy categories you have!


Let me start getting to my point here – big guys lift big weights (generally) \-\> case and point below (although the relationship is a little weaker in women). Let’s see how this shows when we plot bodyweight vs. total weight lifted


![13](data_artifacts/tidytuesday/2019-10-08/images/13.png)![14](data_artifacts/tidytuesday/2019-10-08/images/14.png)


But what is the distribution of weight in different ages? Do we start seeing less heavy lifters when we get to older ages? That was suggested by our plot above, but let’s visualize it in groups of ages as well.


![15](data_artifacts/tidytuesday/2019-10-08/images/15.png)![16](data_artifacts/tidytuesday/2019-10-08/images/16.png)


Look above. What you see is that the mean weights do decrease slightly with age for both men and women…but! The upper end of those violins shows you those heavy lifters we talk about! You clearly see that when we reach 50 and 60s or so, there are very few really heavy men and women. Hmmm!


Let’s look at the same type of relationship in total weight lifted. I think when we compare maximum weight lifted in each age category and compare those, the relationship is way different than if we compare the means in each category These two metrics paint two separate pictures and I think bodyweight may be part of the explanation (at least in this dataset).


What you see below is the median total weight lifted in each weight category, as well as the maximum weight lifted for men.


![17](data_artifacts/tidytuesday/2019-10-08/images/17.png)![18](data_artifacts/tidytuesday/2019-10-08/images/18.png)


What you see is that the maximum weight lifted in each category declines much more rapidly than the average weight. This does differ between Equipment type with Raw being the smoothest decline and Multi\-ply seeming to be the strongest


As example let’s take the difference between average 25\-29 category and 50\-54



```
## $`Multi-ply`
## [1] 64.045
## 
## $Raw
## [1] 55
## 
## $`Single-ply`
## [1] 90
## 
## $Wraps
## [1] 85

```


```
## $`Multi-ply`
## [1] 317.52
## 
## $Raw
## [1] 177.5
## 
## $`Single-ply`
## [1] 250
## 
## $Wraps
## [1] 207.82

```

What you see here are the differences between median and then maximum weight lifted at those two age categories. When we look at median, you see \<90kg difference in all categories, and it is as small as 55 kg difference in mean total weight lifted in the raw division


When we look at maximums – **large** differences appear! Raw is still with the smallest difference of 177\.5kg, while Multi\-ply lifters lift 317\.52 kg more as a maximum of the 25\-29kg category than the maximum in the 50\-55\. What this means is that the average weight lifted by older lifters is lower, but not by an insane amount. On the other hand, there are very few older lifters that lift huge weights as the younger categories do. **WHY**?


Let’s confirm if there is a similar trend in women before we start answering that question!


![19](data_artifacts/tidytuesday/2019-10-08/images/19.png)![20](data_artifacts/tidytuesday/2019-10-08/images/20.png)


*Absolutely* there is! I’m going to put some numbers to it again.



```
## $`Multi-ply`
## [1] 0
## 
## $Raw
## [1] 37.5
## 
## $`Single-ply`
## [1] 90
## 
## $Wraps
## [1] 41.25

```


```
## $`Multi-ply`
## [1] 165.41
## 
## $Raw
## [1] 118.5
## 
## $`Single-ply`
## [1] 153
## 
## $Wraps
## [1] 225.5

```

We see that there is *NO* difference between median Multi\-ply lifts between age ranges of 25\-29 and 50\-54, but over 165Kg difference in maximum lift!! There is again a much more stark difference between maximums at those age ranges, than there is in medians.


Let’s resubset our data and see who is lifting those weights and how much do they weigh compared to their max counterparts in the older categories


![21](data_artifacts/tidytuesday/2019-10-08/images/211.png)  

If that doesn’t show it, what does. The size and redness of the dot is the weight of the lifter who made a maximum lift. As you get to the older categories, what you see is a consistent decline in both maximum lift and in weight of the lifter, who lifted that maximum weight.


Let’s show this a little more explicitly with a relationship between weight lifted and weight of lifter


![22](data_artifacts/tidytuesday/2019-10-08/images/22.png)



```
## 
## Call:
## lm(formula = max_lifts ~ BodyweightKg, data = max2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -361.99 -141.50  -13.73  132.35  510.13 
## 
## Coefficients:
##               Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  -108.7773   107.8276  -1.009    0.318    
## BodyweightKg    7.8187     0.8732   8.954 4.85e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 184.6 on 51 degrees of freedom
## Multiple R-squared:  0.6112, Adjusted R-squared:  0.6036 
## F-statistic: 80.17 on 1 and 51 DF,  p-value: 4.855e-12

```

What you see is a **rather strong** correlation between weight of the lifter and the weight the lifter lifted. Remember, these are the **BEST** lifters of their Age range from among 150 000 entries! We see that 65% of variability between lifters is purely explained by their weight! That’s a lot of percent! And this is a significant relationship as well. This is even disregarding equipment types (which I checked and they only explain an extra 5% of the relationship). This is *huge* because it suggests that age may be important for how much you lift, but your bodyweight carries a much higher significance in terms of those huge numbers you see in the younger age categories.


Let’s check on this with the women lifter data.


![23](data_artifacts/tidytuesday/2019-10-08/images/23.png)  

This is not as convincing as the male data, but the overall trend is similar. Remember, in women there is also a much smaller effect of age on total weight lifted too. And a smaller relationship between weight and total weight lifted.


Let’s see the more explicit plot.


![24](data_artifacts/tidytuesday/2019-10-08/images/24.png)



```
## 
## Call:
## lm(formula = max_lifts ~ BodyweightKg + Equipment, data = max2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -280.33  -82.39   32.16   95.18  230.37 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          277.9507    84.1928   3.301 0.002031 ** 
## BodyweightKg           4.3650     0.9729   4.487 5.98e-05 ***
## EquipmentRaw        -233.1985    62.1342  -3.753 0.000555 ***
## EquipmentSingle-ply -151.9426    70.6037  -2.152 0.037483 *  
## EquipmentWraps      -159.2045    63.3078  -2.515 0.016033 *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 142 on 40 degrees of freedom
## Multiple R-squared:  0.4333, Adjusted R-squared:  0.3766 
## F-statistic: 7.646 on 4 and 40 DF,  p-value: 0.0001128

```

This is relatively consistent! A bit more noise than the male data, explaining only 20% of data. When we include Equipment this goes up to 38% of total data explained. Not as convincing, but still significant.


Now one last thing that we need to see is if this is consistent within weight classes between ages. This is a separate analysis that will take us away from who is doing the best lifts, and lead us to better understand how people of the same weight are doing over time.


Let’s first look at performance of lifters in weightlcasses. This will give us an idea if we have certain weight classes more represented in younger ages than older ages.


Let’s try to plot these up in a meaningful way that will allow us to see progression through the age in the same weight groups.


![25](data_artifacts/tidytuesday/2019-10-08/images/25.png)



```
## 
## Call:
## lm(formula = max_lifts ~ BodyweightKg, data = max2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -366.16  -79.94   22.67  110.51  320.23 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  218.5400    89.3209   2.447 0.018581 *  
## BodyweightKg   3.4304     0.9577   3.582 0.000863 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 159.7 on 43 degrees of freedom
## Multiple R-squared:  0.2298, Adjusted R-squared:  0.2119 
## F-statistic: 12.83 on 1 and 43 DF,  p-value: 0.0008634

```

![26](data_artifacts/tidytuesday/2019-10-08/images/26.png)


You can start seeing the trends here. The heaviest of people are no longer present in the older age groups. You can see this by the disappearance of the violin plots of pinkish, bluish color as you get to the older age groups. Now this is starting to tell us that those max lifter monsters that are really heavy and make the big lifts, either no longer compete later, or they lose weight as they age. Now let’s see that distribution broken down into age groups over time a little more clearly.


I’ve taken here the most represented group over time the 86\-95kg group in men and the 56\-75kg group in women. Then I’ve plotted the total weights they lift as they age to see how the same group performs over time.


![27](data_artifacts/tidytuesday/2019-10-08/images/27.png)![28](data_artifacts/tidytuesday/2019-10-08/images/28.png)



```
## (Intercept)         Age 
##   717.52533    -3.18427

```


```
## (Intercept)         Age 
##  389.730230   -1.611683

```

Above I am showing you the performances of people in the same weight group as they age for men (top) and women (bottom). Well y’all this seems just idealistic for me… There’s a decline in performance with age, but that decline is not really that incredible, compared to what we saw above in terms of the decline of performance with weight. The means age performance declines rather slowly and while overall 25 year olds definitely perform better, there are a good number of 50\+ year olds that perform above the 25yo average.


So can you still lift well as you get older?
--------------------------------------------


What we see in this dataset is that Age does matter in the amount of weight that you lift…but not ras much as you might think! It is dependent on which type of lifting you do (Multi\-ply, Raw…). But overall, the avearage lifts for ages don’t really drop by much with time. We are talking in the range of 3kg/year for men and 1\.6 kg/year for women! For men in 30 years that’s 60kg or 132 lbs. In a hypothetical if you started with 1500 total at 25, at 55 you can still pull a nice 1350 (ON AVERAGE). For women that’s a decline of 48kg or 115lbs. Start with a 1000lbs, go to 885 at 55\. Not bad eh! I mean I’d love to see a 55 year old at my gym who can pull 500 lbs, and this data seems to suggest that this is highly doable!


Let me make this clear – these are trends! This doesn’t say that with a lot of training and good regimen you can’t keep or excede your gains past a certain point! Maybe when you get to your 60s it will get more difficult as these trends show a steep dropoff at that point.. The bigger influence on your lifts are your weight. That being said:


**DON’T TRY TO FATTEN UP JUST TO LIFT MORE** especially as you get older. That comes with many health outcomes, so DO NOT TAKE THIS AWAY FROM THIS DATA. What you can take away from here is that if you plan to keep your weight, you don’t have to stop lifting. You’re not really likely to lose your *gainz* over time by very much.


I want to absolutely acknowledge that this is data of likely trained lifters. If you’re competing in your 50s and 60s, you’re likely to be a seasoned powerlifter, so don’t compare your numbers too harshly to everyone here. These folks are good!


Final message that I think is well supported with this data – don’t stop lifting, don’t stop asking questions!




---


PS:
===


Younglings
----------


For shits ang giggles let’s verify why I threw out the data of people under 22\.


* They create a hump in the distribution of Total weight lifted because they are still getting stronger. If we plot these side by side, you can see that lifters get stronger till about 23\-25 and then plateau there.


![29](data_artifacts/tidytuesday/2019-10-08/images/29.png)



```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = men3)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -677.87  -61.04    0.61   61.70  449.85 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          -26.23804    6.06224  -4.328 1.51e-05 ***
## Age                   18.98153    0.14926 127.173  < 2e-16 ***
## BodyweightKg           3.56664    0.02074 171.999  < 2e-16 ***
## EquipmentRaw        -141.29413    5.08609 -27.780  < 2e-16 ***
## EquipmentSingle-ply  -61.31487    5.10453 -12.012  < 2e-16 ***
## EquipmentWraps      -116.37323    5.17015 -22.509  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 95.58 on 57815 degrees of freedom
##   (279 observations deleted due to missingness)
## Multiple R-squared:  0.5324, Adjusted R-squared:  0.5323 
## F-statistic: 1.316e+04 on 5 and 57815 DF,  p-value: < 2.2e-16

```

![30](data_artifacts/tidytuesday/2019-10-08/images/30.png)



```
## 
## Call:
## lm(formula = TotalKg ~ Age + BodyweightKg + Equipment, data = women3)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -314.42  -40.58   -1.59   39.55  318.05 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          48.50689    8.71955   5.563 2.68e-08 ***
## Age                   8.69720    0.14493  60.012  < 2e-16 ***
## BodyweightKg          2.37514    0.02706  87.772  < 2e-16 ***
## EquipmentRaw        -86.42143    8.09560 -10.675  < 2e-16 ***
## EquipmentSingle-ply   0.67369    8.10626   0.083    0.934    
## EquipmentWraps      -76.46058    8.19974  -9.325  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 64.6 on 22762 degrees of freedom
##   (63 observations deleted due to missingness)
## Multiple R-squared:  0.4606, Adjusted R-squared:  0.4605 
## F-statistic:  3887 on 5 and 22762 DF,  p-value: < 2.2e-16

```

* The linear model here reveals a strong positive relationship of both Age and Weight.


In the spirit of open science, please find all of the code used to create this here: [power\_2\_code](https://oziolor.wordpress.com/wp-content/uploads/2018/05/power_2_code.pdf "power_2_code")!




 
### Share this:

* [Twitter](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?share=twitter "Click to share on Twitter")
* [Facebook](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?share=facebook "Click to share on Facebook")
* 
Like Loading...

### *Related*


 

 [theympblog](https://oziolor.wordpress.com/author/theympblog/)[May 19, 2018December 3, 2018](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/) 


3 thoughts on “Part I: Getting old? You can still lift!”
--------------------------------------------------------


1. **bearystrongstefan** says: 

[May 22, 2018 at 9:21 am](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/#comment-2) 


Very cool work, thanks :)!


[Like](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?like_comment=2&_wpnonce=a5bd0fef14)Like



[Reply](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?replytocom=2#respond) 
	1. **[theympblog](https://oziolor.wordpress.com)** says: 
	
	[May 22, 2018 at 12:55 pm](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/#comment-3) 
	
	
	Absolutely, I’m glad you liked the article! Let me know if there are any other trends you’d be interested in knowing about powerlifters and stay tuned for some more articles coming out of this dataset!
	
	
	[Like](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?like_comment=3&_wpnonce=40da49572f)Like
	
	
	
	[Reply](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?replytocom=3#respond)
	3. **Francis Clark** says: 
	
	[May 25, 2019 at 12:41 am](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/#comment-63) 
	
	
	Being an old guy I love this analysis. I was a powerlifter (@90k \& 100k) I’m 65 now and I still bench heavy. I think injuries really cull the herd on the age axis. My knees and my lower back have been injured over the years so I can not squat or deadlift competitively. I don’t think you can quantify to what extent injuries, rather than the aging process itself impact performance? Or do you consider it one and the same? I don’t know even one old lifter who doesn’t complain constantly about bad knees, back, or shoulders. I guess it is the price we pay for a lifetime of lifting heavy objects repetitively. That being said, I went to my 45th high school reunion in 2017 and I couldn’t believe how feeble some of my classmates appeared. Guess I’ll keep doing what I’m doing, please continue with your insightful analysis.  
	
	Thank you  
	
	Francis Clark
	
	
	[Like](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?like_comment=63&_wpnonce=714f391a38)Like
	
	
	
	[Reply](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/?replytocom=63#respond)



### Leave a comment [Cancel reply](/2018/05/19/part-i-getting-old-you-can-still-lift/#respond)





Δ

 


Post navigation
---------------


[Previous Previous post: Powerful Data Project Intro](https://oziolor.wordpress.com/2018/05/17/powerful-data-project-intro/)[Next Next post: Powerful Data Part II: How much stronger do steroids really make you?](https://oziolor.wordpress.com/2018/07/29/powerful-data-part-ii-how-much-stronger-do-steroids-really-make-you/)



Sidebar

Current status
--------------

 Hi folks,


I am currently a postdoc in [Dr. Andrew Whitehead](https://whiteheadresearch.wordpress.com/)‘s lab. Here I am exploring Pacific herring demographic collapse through time\-series population genomics. I am continuing my growth in the field of evolutionary toxicology and population genomics and hoping to find a place to house my own lab in the near future.


\-Elias





Search for:





Recent Posts
------------


* [Powerful Data Part II: How much stronger do steroids really make you?](https://oziolor.wordpress.com/2018/07/29/powerful-data-part-ii-how-much-stronger-do-steroids-really-make-you/)
July 29, 2018
* [Part I: Getting old? You can still lift!](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/)
May 19, 2018
* [Powerful Data Project Intro](https://oziolor.wordpress.com/2018/05/17/powerful-data-project-intro/)
May 17, 2018
* [Distribution of industrial contamination in a bay system](https://oziolor.wordpress.com/2018/03/07/distribution-of-industrial-contamination-in-a-bay-system/)
March 7, 2018
* [New study out – Biomarkers of exposure and effect in tree swallow at areas of concern in the Great Lakes](https://oziolor.wordpress.com/2017/10/21/new-study-out-biomarkers-of-exposure-and-effect-in-tree-swallow-at-areas-of-concern-in-the-great-lakes/)
October 21, 2017


 




* [GitHub](http://github.com/eoziolor)
 


[Create a free website or blog at WordPress.com.](https://wordpress.com/?ref=footer_website)


















 



* [Comment](https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/#comments)
* Reblog
* Subscribe
Subscribed




	+ [Elias Oziolor, Ph.D.](https://oziolor.wordpress.com)







 

 Sign me up 


* Already have a WordPress.com account? [Log in now.](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Foziolor.wordpress.com%2F2018%2F05%2F19%2Fpart-i-getting-old-you-can-still-lift%2F&signup_flow=account)
* [Privacy](#)
* + [Elias Oziolor, Ph.D.](https://oziolor.wordpress.com)
	+ [Customize](https://oziolor.wordpress.com/wp-admin/customize.php?url=https%3A%2F%2Foziolor.wordpress.com%2F2018%2F05%2F19%2Fpart-i-getting-old-you-can-still-lift%2F)
	+ Subscribe
	Subscribed
	+ [Sign up](https://wordpress.com/start/)
	+ [Log in](https://wordpress.com/log-in?redirect_to=https%3A%2F%2Foziolor.wordpress.com%2F2018%2F05%2F19%2Fpart-i-getting-old-you-can-still-lift%2F&signup_flow=account)
	+ [Copy shortlink](https://wp.me/p9a1qS-22)
	+ [Report this content](https://wordpress.com/abuse/?report_url=https://oziolor.wordpress.com/2018/05/19/part-i-getting-old-you-can-still-lift/)
	+ [View post in Reader](https://wordpress.com/read/blogs/135375814/posts/126)
	+ [Manage subscriptions](https://subscribe.wordpress.com/)
	+ Collapse this bar






 





























































Loading Comments...



 


Write a Comment...




Email (Required)



Name (Required)



Website











### 
























 


%d 



 

Design a site like this with WordPress.com[Get started](https://wordpress.com/start/?ref=marketing_bar) 




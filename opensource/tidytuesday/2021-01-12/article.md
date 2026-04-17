






Aspect Ratio of Artworks through Time





















Aspect Ratio of Artworks through Time
=====================================


#### *Joseph Lewis*


#### *30 January 2018*




* [Questions](#questions)
* [Data](#data)
* [Exploration](#exploration)
	+ [Year of Artwork Creation versus Year Acquired by Tate Gallery](#year-of-artwork-creation-versus-year-acquired-by-tate-gallery)
	+ [Pre\-Tate Gallery Artwork Acqusition](#pre-tate-gallery-artwork-acqusition)
* [Aspect Ratio through Time](#aspect-ratio-through-time)
	+ [The Rise of Postmodernism](#the-rise-of-postmodernism)
* [Using Aspect Ratio to Predict Year of Artwork Creation](#using-aspect-ratio-to-predict-year-of-artwork-creation)





---



Questions
=========


* How have the aspect ratio (width of artwork / height of artwork) of paintings changed throughout time?
* Can the aspect ratio of artworks be used to predict when the paintings were created?




---




Data
====


The Tate Collection dataset contains \~70,000 artworks that are owned or partly owned by Tate. [Data Source](https://www.kaggle.com/rtatman/the-tate-collection/data)




---




Exploration
===========




---



```
library(ggplot2)
library(scales)
library(caTools)
library(randomForest)
library(caret)
library(e1071)
```

Load data and check structure



```
artworks <- read.csv("the-tate-collection.csv", stringsAsFactors = FALSE, sep = ";")

str(artworks)
```


```
## 'data.frame':    69201 obs. of  20 variables:
##  $ id                : int  20400 20618 20830 21086 21163 21157 21153 21210 21271 21405 ...
##  $ accession_number  : chr  "P77527" "P77580" "P77612" "P77680" ...
##  $ artist            : chr  "Charlton, Alan" "Artschwager, Richard" "Marden, Brice" "Francis, Mark" ...
##  $ artistRole        : chr  "artist" "artist" "artist" "artist" ...
##  $ artistId          : int  891 669 1578 2311 1922 2170 2170 1938 2146 2339 ...
##  $ title             : chr  "[no title]" "Interior" "[no title]" "Untitled" ...
##  $ dateText          : chr  "1991" "1972" "1971" "1994" ...
##  $ medium            : chr  "Screenprint on paper" "Screenprint on paper" "Etching and aquatint on paper" "Monotype on paper" ...
##  $ creditLine        : chr  "Purchased 1992" "Purchased 1992" "Purchased 1993" "Purchased 1994" ...
##  $ year              : int  1991 1972 1971 1994 1968 1994 1994 1982 1994 1988 ...
##  $ acquisitionYear   : int  1992 1992 1993 1994 1994 1994 1994 1983 1995 1995 ...
##  $ dimensions        : chr  "image: 362 x 362 mm" "image: 715 x 1043 mm" "image: 370 x 603 mm" "image: 582 x 584 mm" ...
##  $ width             : int  362 715 370 582 1044 380 383 1147 544 585 ...
##  $ height            : int  362 1043 603 584 681 356 362 760 641 418 ...
##  $ depth             : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ units             : chr  "mm" "mm" "mm" "mm" ...
##  $ inscription       : chr  "date inscribed" "date inscribed" "date inscribed" "" ...
##  $ thumbnailCopyright: chr  "Â© Alan Charlton" "Â© ARS, NY and DACS, London 2014" "Â© ARS, NY and DACS, London 2014" "Â© Mark Francis" ...
##  $ thumbnailUrl      : chr  "https://data.opendatasoft.com/api/datasets/1.0/the-tate-collection@public/images/a76355ec5781715e41cb08f1780b5ab0" "https://data.opendatasoft.com/api/datasets/1.0/the-tate-collection@public/images/d1875557c1a8dada3e60984cd0447cd7" "https://data.opendatasoft.com/api/datasets/1.0/the-tate-collection@public/images/cffeaa9f8a80028d928d47763167ad8a" "https://data.opendatasoft.com/api/datasets/1.0/the-tate-collection@public/images/c0ada25718520babc378ab32ebd9b811" ...
##  $ url               : chr  "http://www.tate.org.uk/art/artworks/charlton-no-title-p77527" "http://www.tate.org.uk/art/artworks/artschwager-interior-p77580" "http://www.tate.org.uk/art/artworks/marden-no-title-p77612" "http://www.tate.org.uk/art/artworks/francis-untitled-p77680" ...
```

Remove unneeded columns.



```
drop <- c("accession_number", "artistRole", "artistId", "dateText", "creditLine", "units", "inscription", "thumbnailCopyright", "thumbnailUrl", "url")
artworks_rem <- artworks[ , !(names(artworks) %in% drop)]

str(artworks_rem)
```


```
## 'data.frame':    69201 obs. of  10 variables:
##  $ id             : int  20400 20618 20830 21086 21163 21157 21153 21210 21271 21405 ...
##  $ artist         : chr  "Charlton, Alan" "Artschwager, Richard" "Marden, Brice" "Francis, Mark" ...
##  $ title          : chr  "[no title]" "Interior" "[no title]" "Untitled" ...
##  $ medium         : chr  "Screenprint on paper" "Screenprint on paper" "Etching and aquatint on paper" "Monotype on paper" ...
##  $ year           : int  1991 1972 1971 1994 1968 1994 1994 1982 1994 1988 ...
##  $ acquisitionYear: int  1992 1992 1993 1994 1994 1994 1994 1983 1995 1995 ...
##  $ dimensions     : chr  "image: 362 x 362 mm" "image: 715 x 1043 mm" "image: 370 x 603 mm" "image: 582 x 584 mm" ...
##  $ width          : int  362 715 370 582 1044 380 383 1147 544 585 ...
##  $ height         : int  362 1043 603 584 681 356 362 760 641 418 ...
##  $ depth          : num  NA NA NA NA NA NA NA NA NA NA ...
```


```
ggplot(artworks_rem) + 
  geom_density(aes(year, fill = "red"), alpha = 0.3) + 
  geom_density(aes(acquisitionYear, fill = "blue"), alpha = 0.3) +
  scale_fill_manual(name = NULL, values = c("red" = "red", "blue" = "blue"), labels=c("blue" = "Acquisition Year", "red" = "Year Artwork Created")) + 
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/0.png)


As seen from the above density plot, there are two peaks of both acquisition year that Tate brought the artwork, and the age of the artworks within the Tate Collection. Interestingly, the first large number of acquisitions occured mid\-19th Century, whilst the second happened in the late 20th Century. The first peak of artworks with acquisition years \~1880 can only contain artworks prior to this. The second peak, which occurs in \~1980s, however could contain artworks from any previous years. Thus, the year of the painting and acquisition year will be explored deeper.




---



Year of Artwork Creation versus Year Acquired by Tate Gallery
-------------------------------------------------------------




---



```
artworks_rem$halfcentury <- cut(artworks_rem$acquisitionYear, breaks = c(1800, 1850, 1900, 1950, 2000, 2050),labels = c("1800-1849", "1850-1899", "1900-1949", "1950-1999", "2000-2050"), include.lowest = TRUE)

ggplot(artworks_rem, aes(year)) +
  geom_histogram(aes(fill = halfcentury), bins = 50) + 
  labs(fill = "Year Artwork Acquired", y = "Count of Artworks") + 
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/1.png)


From this, it appears that the majority of artworks that were created in the early 19th Century were also acquired in the same period, with relatively few 19th century artworks being acquired in periods later than this. Similarly, artworks created in the mid\-20th Century were also acquired at this time. The later surge of acquisitions coincide with the renaming of the National Gallery of British Art to the Tate Gallery, which occured in 1932\. As the Tate Gallery first opened in 1897, the acquisition years before this are likely due to the data also containing artworks that are jointly owned by the National Galleries of Scotland.




---




Pre\-Tate Gallery Artwork Acqusition
------------------------------------



```
artworks_pre_tate <- artworks_rem[artworks_rem$year <= 1897,]

ggplot(artworks_pre_tate) +
  geom_histogram(aes(year), bins = 30) +
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/2.png)


Let’s see what artists makes up the pre\-Tate collection.



```
sort(table(artworks_pre_tate$artist), decreasing = T)[1:5]
```


```
## 
## Turner, Joseph Mallord William               Daniell, William 
##                          39046                            612 
##                Constable, John                 Blake, William 
##                            188                            175 
##                  Flaxman, John 
##                            151
```


```
sort(table(artworks_pre_tate$artist), decreasing = T)[1] / sum(table(artworks_pre_tate$artist))
```


```
## Turner, Joseph Mallord William 
##                      0.8892077
```

There appears to be a lot of artworks by Turner, making up 89% of the pre\-Tate collection. Let’s explore this further.



```
ggplot(artworks_pre_tate) +
  geom_histogram(aes(year, fill = artist == "Turner, Joseph Mallord William"), bins = 30) +
  labs(fill = "Artwork by JMW Turner?") +
  theme_bw()
```

![](path/not/found)



```
artworks_turner <- artworks_pre_tate[artworks_pre_tate$artist == "Turner, Joseph Mallord William",]

ggplot(artworks_turner) +
  geom_histogram(aes(year, fill = artworks_turner$halfcentury), bins = 30) + 
  labs(fill = "Year Artwork Acquired", y = "Count of Artworks") + 
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/4.png)


Much like previously found, with the majority of artworks being acquired close to when they were created, the vast majority of artworks by Turner were acquired just after his death in 1851, through the “Turner Bequest”, in which he donated his artworks to the National Gallery, which are now mostly housed in the Clore Gallery at Tate Britain.




---





Aspect Ratio through Time
=========================




---


Creation of the aspect ratio (height of artwork / width of artwork)



```
artworks_ar <- artworks_rem[!(is.na(artworks_rem$height & artworks_rem$width &artworks_rem$year)), ]

artworks_ar$aspectratio <- artworks_ar$height / artworks_ar$width

ggplot(artworks_ar) +
  geom_point(aes(year, aspectratio)) + 
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/5.png)


As seen from above, the aspect ratio of artworks within the Tate are relatively static. That is, until \~1950s, where the aspect ratios of some artworks changes dramatically.


One artwork, in particular, has an aspect ratio of \> 3000\. Let’s check to see whether this is an error in the data, or in fact a real artwork.



```
artworks_ar <- artworks_ar[order(artworks_ar$aspectratio),]

artworks_ar[artworks_ar$aspectratio > 3000,]
```


```
##          id          artist              title medium year acquisitionYear
## 40103 21561 Balka, Miroslaw [diameter]1 x 3750  Steel 1995            1996
##                            dimensions width height depth halfcentury
## 40103 unconfirmed: 10 x 37500 x 10 mm    10  37500    10   1950-1999
##       aspectratio
## 40103        3750
```

From above, it is in fact a real artwork. Created by Balka in 1995, the piece, according to Tate Gallery, conceptulises grief and memory.







---



The Rise of Postmodernism
-------------------------




---



```
artworks_ar_1950 <- artworks_ar[artworks_ar$year >= 1950,]

ggplot(artworks_ar_1950) +
  geom_point(aes(year, aspectratio)) + 
  theme_bw()
```

![](opensource/tidytuesday/2021-01-12/images/6.png)


As seen above, the 1950s onwards saw artworks with greater aspect ratios.


This is seen further by visualising the actual shape of the paintings.



```
artworks_ar$postmodern <- ifelse(artworks_ar$year >= 1950, 'yes', 'no')

artworks_ar <- artworks_ar[rev(order(artworks_ar$postmodern)),]

ggplot(artworks_ar, aes(xmin = 0, xmax = width, ymin = 0, ymax = height, color = postmodern)) +
  geom_rect(alpha = 0) +
  labs(color="Postmodern?", x = "Width", y = "Height") +
  theme_bw()
```

![](path/not/found)




---





Using Aspect Ratio to Predict Year of Artwork Creation
======================================================




---



```
artworks_ar$century <- cut(artworks_ar$year, breaks = c(1500,1550,1600,1650,1700,1750,1800,1850,1900,1950,2000,2050),labels = c("1500-1549", "1550-1600","1600-1649","1650-1699","1700-1749","1750-1799","1800-1849","1850-1899","1900-1949", "1950-1999","2000-2050"), include.lowest = TRUE)

sample <- sample.split(artworks_ar$century, SplitRatio=0.7)

train <- artworks_ar[sample,]
test  <- artworks_ar[!sample,]
```


```
rf <-  randomForest(train$century ~ aspectratio, ntree = 500, data = train)

print(rf)
```


```
## 
## Call:
##  randomForest(formula = train$century ~ aspectratio, data = train,      ntree = 500) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 1
## 
##         OOB estimate of  error rate: 23.2%
## Confusion matrix:
##           1500-1549 1550-1600 1600-1649 1650-1699 1700-1749 1750-1799
## 1500-1549         0         0         0         0         0         0
## 1550-1600         0         0         0         0         0         1
## 1600-1649         0         0         0         0         0         1
## 1650-1699         0         0         0         0         0         4
## 1700-1749         0         0         0         0         5        11
## 1750-1799         0         0         1         1         8      1864
## 1800-1849         0         2         2         2        29       267
## 1850-1899         0         0         2         1         8        37
## 1900-1949         0         0         6         6        13       158
## 1950-1999         1         8         9        14        46       421
## 2000-2050         0         0         0         1         2        22
##           1800-1849 1850-1899 1900-1949 1950-1999 2000-2050 class.error
## 1500-1549         0         0         0         1         0   1.0000000
## 1550-1600         2         0         0         7         0   1.0000000
## 1600-1649         4         1         5        16         0   1.0000000
## 1650-1699         6         1         5        17         1   1.0000000
## 1700-1749        28         5        18        49         4   0.9583333
## 1750-1799       523        28       112       350        26   0.3601099
## 1800-1849     24128       148       302      1105        79   0.0742787
## 1850-1899       273        97       142       372        25   0.8986416
## 1900-1949       497       116       609      1037        56   0.7562050
## 1950-1999      1754       285       874      6106       199   0.3716168
## 2000-2050       119        16        48       272       338   0.5867971
```


```
train$predicted_response <- predict(rf, train)

print(confusionMatrix(data = train$predicted_response,reference = train$century))
```


```
## Confusion Matrix and Statistics
## 
##            Reference
## Prediction  1500-1549 1550-1600 1600-1649 1650-1699 1700-1749 1750-1799
##   1500-1549         1         0         0         0         0         0
##   1550-1600         0         8         0         0         0         0
##   1600-1649         0         0        21         0         0         0
##   1650-1699         0         0         0        23         0         0
##   1700-1749         0         0         0         0        92         1
##   1750-1799         0         0         0         1         2      2535
##   1800-1849         0         1         0         3        13       290
##   1850-1899         0         0         0         0         2         1
##   1900-1949         0         0         0         1         4        11
##   1950-1999         0         1         6         6         6        66
##   2000-2050         0         0         0         0         1         9
##            Reference
## Prediction  1800-1849 1850-1899 1900-1949 1950-1999 2000-2050
##   1500-1549         0         0         0         0         0
##   1550-1600         0         0         0         0         0
##   1600-1649         0         0         1         0         0
##   1650-1699         0         0         0         0         0
##   1700-1749         1         2         4         6         0
##   1750-1799        83        16        62       113         8
##   1800-1849     25657       110       236       677        59
##   1850-1899         8       660        25        23         1
##   1900-1949        50        45      1806       130         5
##   1950-1999       246       118       343      8734       132
##   2000-2050        19         6        21        34       613
## 
## Overall Statistics
##                                           
##                Accuracy : 0.9303          
##                  95% CI : (0.9278, 0.9327)
##     No Information Rate : 0.6039          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.8762          
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: 1500-1549 Class: 1550-1600 Class: 1600-1649
## Sensitivity                 1.000e+00        0.8000000        0.7777778
## Specificity                 1.000e+00        1.0000000        0.9999768
## Pos Pred Value              1.000e+00        1.0000000        0.9545455
## Neg Pred Value              1.000e+00        0.9999537        0.9998609
## Prevalence                  2.317e-05        0.0002317        0.0006256
## Detection Rate              2.317e-05        0.0001854        0.0004866
## Detection Prevalence        2.317e-05        0.0001854        0.0005097
## Balanced Accuracy           1.000e+00        0.9000000        0.8888773
##                      Class: 1650-1699 Class: 1700-1749 Class: 1750-1799
## Sensitivity                 0.6764706         0.766667          0.87024
## Specificity                 1.0000000         0.999675          0.99292
## Pos Pred Value              1.0000000         0.867925          0.89894
## Neg Pred Value              0.9997450         0.999350          0.99063
## Prevalence                  0.0007878         0.002780          0.06749
## Detection Rate              0.0005329         0.002132          0.05874
## Detection Prevalence        0.0005329         0.002456          0.06534
## Balanced Accuracy           0.8382353         0.883171          0.93158
##                      Class: 1800-1849 Class: 1850-1899 Class: 1900-1949
## Sensitivity                    0.9844          0.68966          0.72298
## Specificity                    0.9187          0.99858          0.99395
## Pos Pred Value                 0.9486          0.91667          0.88012
## Neg Pred Value                 0.9747          0.99300          0.98317
## Prevalence                     0.6039          0.02217          0.05788
## Detection Rate                 0.5945          0.01529          0.04185
## Detection Prevalence           0.6267          0.01668          0.04755
## Balanced Accuracy              0.9516          0.84412          0.85846
##                      Class: 1950-1999 Class: 2000-2050
## Sensitivity                    0.8988          0.74939
## Specificity                    0.9724          0.99787
## Pos Pred Value                 0.9043          0.87198
## Neg Pred Value                 0.9707          0.99517
## Prevalence                     0.2251          0.01895
## Detection Rate                 0.2024          0.01420
## Detection Prevalence           0.2238          0.01629
## Balanced Accuracy              0.9356          0.87363
```


```
test$predicted_response <- predict(rf, test)

print(confusionMatrix(data=test$predicted_response, reference=test$century))
```


```
## Confusion Matrix and Statistics
## 
##            Reference
## Prediction  1500-1549 1550-1600 1600-1649 1650-1699 1700-1749 1750-1799
##   1500-1549         0         0         0         0         0         0
##   1550-1600         0         0         0         0         0         0
##   1600-1649         0         0         0         0         0         2
##   1650-1699         0         0         0         0         0         1
##   1700-1749         0         0         0         1         1         3
##   1750-1799         0         0         3         0         5       791
##   1800-1849         0         0         2         2        16       220
##   1850-1899         0         0         0         1         3        17
##   1900-1949         0         0         0         3         4        48
##   1950-1999         1         4         7         8        21       156
##   2000-2050         0         0         0         0         1        11
##            Reference
## Prediction  1800-1849 1850-1899 1900-1949 1950-1999 2000-2050
##   1500-1549         0         0         0         0         0
##   1550-1600         1         1         0         1         0
##   1600-1649         1         1         0         7         0
##   1650-1699         3         0         0         6         0
##   1700-1749         8         2         7        21         0
##   1750-1799       106        14        58       168         8
##   1800-1849     10322       110       253       703        48
##   1850-1899        75        44        57       121         3
##   1900-1949       126        58       253       357        25
##   1950-1999       494       169       422      2702       126
##   2000-2050        35        11        20        78       141
## 
## Overall Statistics
##                                           
##                Accuracy : 0.7706          
##                  95% CI : (0.7644, 0.7766)
##     No Information Rate : 0.6039          
##     P-Value [Acc > NIR] : < 2.2e-16       
##                                           
##                   Kappa : 0.5912          
##  Mcnemar's Test P-Value : NA              
## 
## Statistics by Class:
## 
##                      Class: 1500-1549 Class: 1550-1600 Class: 1600-1649
## Sensitivity                 0.000e+00        0.0000000        0.0000000
## Specificity                 1.000e+00        0.9998378        0.9994050
## Pos Pred Value                    NaN        0.0000000        0.0000000
## Neg Pred Value              9.999e-01        0.9997837        0.9993509
## Prevalence                  5.406e-05        0.0002162        0.0006487
## Detection Rate              0.000e+00        0.0000000        0.0000000
## Detection Prevalence        0.000e+00        0.0001622        0.0005947
## Balanced Accuracy           5.000e-01        0.4999189        0.4997025
##                      Class: 1650-1699 Class: 1700-1749 Class: 1750-1799
## Sensitivity                 0.0000000        1.961e-02          0.63331
## Specificity                 0.9994590        9.977e-01          0.97901
## Pos Pred Value              0.0000000        2.326e-02          0.68604
## Neg Pred Value              0.9991887        9.973e-01          0.97359
## Prevalence                  0.0008109        2.757e-03          0.06752
## Detection Rate              0.0000000        5.406e-05          0.04276
## Detection Prevalence        0.0005406        2.325e-03          0.06233
## Balanced Accuracy           0.4997295        5.087e-01          0.80616
##                      Class: 1800-1849 Class: 1850-1899 Class: 1900-1949
## Sensitivity                    0.9240         0.107317          0.23645
## Specificity                    0.8152         0.984686          0.96437
## Pos Pred Value                 0.8840         0.137072          0.28947
## Neg Pred Value                 0.8755         0.979865          0.95364
## Prevalence                     0.6039         0.022165          0.05784
## Detection Rate                 0.5580         0.002379          0.01368
## Detection Prevalence           0.6312         0.017353          0.04725
## Balanced Accuracy              0.8696         0.546002          0.60041
##                      Class: 1950-1999 Class: 2000-2050
## Sensitivity                    0.6489         0.401709
## Specificity                    0.9018         0.991404
## Pos Pred Value                 0.6574         0.474747
## Neg Pred Value                 0.8984         0.988462
## Prevalence                     0.2251         0.018975
## Detection Rate                 0.1461         0.007622
## Detection Prevalence           0.2222         0.016056
## Balanced Accuracy              0.7753         0.696556
```









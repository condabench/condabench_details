









UCI Machine Learning Repository




Spambase \- UCI Machine Learning Repository




       * [Datasets](/datasets)
* [Contribute Dataset](/contribute/donation)
	+ [Donate New](/contribute/donation)
	+ [Link External](/contribute/linking)
* [About Us](/about)
	+ [Who We Are](/about)
	+ [Citation Metadata](/citation)
	+ [Contact Information](/contact)
           [Login](/auth/login)       Spambase
========

  Donated on 6/30/1999
--------------------

      Classifying Email as Spam or Non\-Spam

  Dataset Characteristics
=======================

 Multivariate

 Subject Area
============

 Computer Science

 Associated Tasks
================

 Classification

 Feature Type
============

 Integer, Real

 \# Instances
============

 4601

 \# Features
===========

 57

   Dataset Information
===================

    What do the instances in this dataset represent?

  Emails

  Additional Information

  The "spam" concept is diverse: advertisements for products/web sites, make money fast schemes, chain letters, pornography...

The classification task for this dataset is to determine whether a given email is spam or not.
 
Our collection of spam e\-mails came from our postmaster and individuals who had filed spam. Our collection of non\-spam e\-mails came from filed work and personal e\-mails, and hence the word 'george' and the area code '650' are indicators of non\-spam. These are useful when constructing a personalized spam filter. One would either have to blind such non\-spam indicators or get a very wide collection of non\-spam to generate a general purpose spam filter.

For background on spam: Cranor, Lorrie F., LaMacchia, Brian A. Spam!, Communications of the ACM, 41(8\):74\-83, 1998\.

Typical performance is around \~7% misclassification error. False positives (marking good mail as spam) are very undesirable.If we insist on zero false positives in the training/testing set, 20\-25% of the spam passed through the filter. See also Hewlett\-Packard Internal\-only Technical Report. External version forthcoming. 

  Has Missing Values?

  Yes 

    Variables Table
===============

     

| Variable Name | Role | Type | Description | Units | Missing Values |
| --- | --- | --- | --- | --- | --- |
| word\_freq\_make | Feature | Continuous |  |  | no |
| word\_freq\_address | Feature | Continuous |  |  | no |
| word\_freq\_all | Feature | Continuous |  |  | no |
| word\_freq\_3d | Feature | Continuous |  |  | no |
| word\_freq\_our | Feature | Continuous |  |  | no |
| word\_freq\_over | Feature | Continuous |  |  | no |
| word\_freq\_remove | Feature | Continuous |  |  | no |
| word\_freq\_internet | Feature | Continuous |  |  | no |
| word\_freq\_order | Feature | Continuous |  |  | no |
| word\_freq\_mail | Feature | Continuous |  |  | no |

 Rows per page 510152025 0 to 10 of 58

    Additional Variable Information
===============================

       The last column of 'spambase.data' denotes whether the e\-mail was considered spam (1\) or not (0\), i.e. unsolicited commercial e\-mail. Most of the attributes indicate whether a particular word or character was frequently occuring in the e\-mail. The run\-length attributes (55\-57\) measure the length of sequences of consecutive capital letters. For the statistical measures of each attribute, see the end of this file. Here are the definitions of the attributes:

48 continuous real \[0,100] attributes of type word\_freq\_WORD 
\= percentage of words in the e\-mail that match WORD, i.e. 100 \* (number of times the WORD appears in the e\-mail) / total number of words in e\-mail. A "word" in this case is any string of alphanumeric characters bounded by non\-alphanumeric characters or end\-of\-string.

6 continuous real \[0,100] attributes of type char\_freq\_CHAR] 
\= percentage of characters in the e\-mail that match CHAR, i.e. 100 \* (number of CHAR occurences) / total characters in e\-mail

1 continuous real \[1,...] attribute of type capital\_run\_length\_average 
\= average length of uninterrupted sequences of capital letters

1 continuous integer \[1,...] attribute of type capital\_run\_length\_longest 
\= length of longest uninterrupted sequence of capital letters

1 continuous integer \[1,...] attribute of type capital\_run\_length\_total 
\= sum of length of uninterrupted sequences of capital letters 
\= total number of capital letters in the e\-mail

1 nominal {0,1} class attribute of type spam
\= denotes whether the e\-mail was considered spam (1\) or not (0\), i.e. unsolicited commercial e\-mail. 


    Baseline Model Performance
==========================

     Accuracy Precision     Dataset Files
=============

    

| File | Size |
| --- | --- |
| spambase.data | 686\.5 KB |
| spambase.DOCUMENTATION | 6\.3 KB |
| spambase.names | 3\.5 KB |

   Papers Citing this Dataset
==========================

     Sort by Year, desc * Title
* Year
* Venue
* Journal
 [Setting decision thresholds when operating conditions are uncertain](https://api.semanticscholar.org/CorpusID:67184677) By Cèsar Ferri, José Hernández\-Orallo, Peter Flach. 2019

 Published in Data Mining and Knowledge Discovery. 

 [Communication\-Efficient Accurate Statistical Estimation](https://api.semanticscholar.org/CorpusID:186206580) By Jianqing Fan, Yongyi Guo, Kaizheng Wang. 2019

 Published in ArXiv. 

 [Explaining Vulnerabilities to Adversarial Machine Learning through Visual Analytics](https://api.semanticscholar.org/CorpusID:197431202) By Yuxin Ma, Tiankai Xie, Jundong Li, Ross Maciejewski. 2019

 Published in ArXiv. 

 [Minimax Optimal Online Stochastic Learning for Sequences of Convex Functions under Sub\-Gradient Observation Failures](https://api.semanticscholar.org/CorpusID:128342895) By Hakan Gokcesu, Suleyman Kozat. 2019

 Published in ArXiv. 

 [Recombinator\-k\-means: Enhancing k\-means\+\+ by seeding from pools of previous runs](https://api.semanticscholar.org/CorpusID:143424878) By Carlo Baldassi. 2019

 Published in ArXiv. 

  Rows per page 52550100200 0 to 5 of 44

    Reviews
=======

    There are no reviews for this dataset yet.

 [Login to Write a Review](/auth/login)   Write a Review
==============

   0  Comments 
```


```
  Submit Cancel     [Download (122\.6 KB)](/static/public/94/spambase.zip)  Import in Python

  Install the ucimlrepo package    
```
pip install ucimlrepo
```
 Import the dataset into your code    
```
from ucimlrepo import fetch_ucirepo 
  
# fetch dataset 
spambase = fetch_ucirepo(id=94) 
  
# data (as pandas dataframes) 
X = spambase.data.features 
y = spambase.data.targets 
  
# metadata 
print(spambase.metadata) 
  
# variable information 
print(spambase.variables) 

```
 [View the full documentation](https://github.com/uci-ml-repo/ucimlrepo) Cite   44 citations  87153 views Citation     
```
Hopkins, M., Reeber, E., Forman, G., & Suermondt, J. (1999). Spambase [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C53G6X.
```
 Style: APAMLAChicagoVancouverIEEEBibTeX    Creators
========

    Mark Hopkins

    Erik Reeber

    George Forman

    Jaap Suermondt

     DOI
===

 [10\.24432/C53G6X](https://doi.org/10.24432/C53G6X)  License
=======

 This dataset is licensed under a
[Creative Commons Attribution 4\.0 International](https://creativecommons.org/licenses/by/4.0/legalcode)
(CC BY 4\.0\) license.

 This allows for the sharing and adaptation of the datasets for any purpose,
provided that the appropriate credit is given.

  By using the UCI Machine Learning Repository,
you acknowledge and accept the cookies and privacy practices used by the UCI Machine Learning Repository.

 Accept [Read Policy](/privacy)  The Project [About Us](/about) [CML](https://cml.ics.uci.edu) [National Science Foundation](https://www.nsf.gov) Navigation [Home](/) [View Datasets](/datasets) [Donate a Dataset](/contribute/donation) Logistics [Contact](/contact) [Privacy Notice](/privacy) [Feature Request or Bug Report](https://github.com/uci-ml-repo/ucimlrepo-feedback/issues/new/choose)  * [Browse Datasets](/datasets)
* [Donate a Dataset](/contribute/donation)
* [Link an external Dataset](/contribute/linking)
* 
* [Who We Are](/about)
* [Citation Metadata](/citation)
* [Contact Information](/contact)
* 
* [Login](/auth/login)








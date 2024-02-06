---
title: "Midterm 1 W24"
author: "Eva Moncada"
date: "2024-02-06"
output:
  html_document: 
    keep_md: yes
  pdf_document: default
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code must be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. 

Your code must knit in order to be considered. If you are stuck and cannot answer a question, then comment out your code and knit the document. You may use your notes, labs, and homework to help you complete this exam. Do not use any other resources- including AI assistance.  

Don't forget to answer any questions that are asked in the prompt!  

Be sure to push your completed midterm to your repository. This exam is worth 30 points.  

## Background
In the data folder, you will find data related to a study on wolf mortality collected by the National Park Service. You should start by reading the `README_NPSwolfdata.pdf` file. This will provide an abstract of the study and an explanation of variables.  

The data are from: Cassidy, Kira et al. (2022). Gray wolf packs and human-caused wolf mortality. [Dryad](https://doi.org/10.5061/dryad.mkkwh713f). 

## Load the libraries

```r
library("tidyverse")
library("janitor")
```

## Load the wolves data
In these data, the authors used `NULL` to represent missing values. I am correcting this for you below and using `janitor` to clean the column names.

```r
wolves <- read.csv("data/NPS_wolfmortalitydata.csv", na = c("NULL")) %>% clean_names()
```

## Questions
Problem 1. (1 point) Let's start with some data exploration. What are the variable (column) names?  


```r
names(wolves)
```

```
##  [1] "park"         "biolyr"       "pack"         "packcode"     "packsize_aug"
##  [6] "mort_yn"      "mort_all"     "mort_lead"    "mort_nonlead" "reprody1"    
## [11] "persisty1"
```

Problem 2. (1 point) Use the function of your choice to summarize the data and get an idea of its structure.  


```r
summary(wolves)
```

```
##      park               biolyr         pack              packcode     
##  Length:864         Min.   :1986   Length:864         Min.   :  2.00  
##  Class :character   1st Qu.:1999   Class :character   1st Qu.: 48.00  
##  Mode  :character   Median :2006   Mode  :character   Median : 86.50  
##                     Mean   :2005                      Mean   : 91.39  
##                     3rd Qu.:2012                      3rd Qu.:133.00  
##                     Max.   :2021                      Max.   :193.00  
##                                                                       
##   packsize_aug       mort_yn          mort_all         mort_lead      
##  Min.   : 0.000   Min.   :0.0000   Min.   : 0.0000   Min.   :0.00000  
##  1st Qu.: 5.000   1st Qu.:0.0000   1st Qu.: 0.0000   1st Qu.:0.00000  
##  Median : 8.000   Median :0.0000   Median : 0.0000   Median :0.00000  
##  Mean   : 8.789   Mean   :0.1956   Mean   : 0.3715   Mean   :0.09552  
##  3rd Qu.:12.000   3rd Qu.:0.0000   3rd Qu.: 0.0000   3rd Qu.:0.00000  
##  Max.   :37.000   Max.   :1.0000   Max.   :24.0000   Max.   :3.00000  
##  NA's   :55                                          NA's   :16       
##   mort_nonlead        reprody1        persisty1     
##  Min.   : 0.0000   Min.   :0.0000   Min.   :0.0000  
##  1st Qu.: 0.0000   1st Qu.:1.0000   1st Qu.:1.0000  
##  Median : 0.0000   Median :1.0000   Median :1.0000  
##  Mean   : 0.2641   Mean   :0.7629   Mean   :0.8865  
##  3rd Qu.: 0.0000   3rd Qu.:1.0000   3rd Qu.:1.0000  
##  Max.   :22.0000   Max.   :1.0000   Max.   :1.0000  
##  NA's   :12        NA's   :71       NA's   :9
```

Problem 3. (3 points) Which parks/ reserves are represented in the data? Don't just use the abstract, pull this information from the data.  


```r
tabyl(wolves, park)
```

```
##  park   n    percent
##  DENA 340 0.39351852
##  GNTP  77 0.08912037
##   VNP  48 0.05555556
##   YNP 248 0.28703704
##  YUCH 151 0.17476852
```

Problem 4. (4 points) Which park has the largest number of wolf packs?


```r
wolves %>% 
  select(park, packsize_aug) %>% 
  group_by(park) %>% 
  arrange(desc(packsize_aug))
```

```
## # A tibble: 864 × 2
## # Groups:   park [5]
##    park  packsize_aug
##    <chr>        <dbl>
##  1 YNP           37  
##  2 YNP           35  
##  3 DENA          33  
##  4 YNP           28  
##  5 DENA          27  
##  6 YNP           27  
##  7 YNP           27  
##  8 GNTP          26.4
##  9 YNP           26  
## 10 YNP           26  
## # ℹ 854 more rows
```

Problem 5. (4 points) Which park has the highest total number of human-caused mortalities `mort_all`?


```r
wolves %>% 
  select(park, mort_all) %>% 
  group_by(park) %>% 
  arrange(desc(mort_all))
```

```
## # A tibble: 864 × 2
## # Groups:   park [5]
##    park  mort_all
##    <chr>    <int>
##  1 YUCH        24
##  2 YUCH        14
##  3 YUCH        12
##  4 YUCH        12
##  5 YUCH        10
##  6 YUCH         8
##  7 YUCH         5
##  8 YUCH         5
##  9 DENA         4
## 10 GNTP         4
## # ℹ 854 more rows
```

The wolves in [Yellowstone National Park](https://www.nps.gov/yell/learn/nature/wolf-restoration.htm) are an incredible conservation success story. Let's focus our attention on this park.  

Problem 6. (2 points) Create a new object "ynp" that only includes the data from Yellowstone National Park. 


```r
ynp <- filter(wolves, park=="YNP")
```



Problem 7. (3 points) Among the Yellowstone wolf packs, the [Druid Peak Pack](https://www.pbs.org/wnet/nature/in-the-valley-of-the-wolves-the-druid-wolf-pack-story/209/) is one of most famous. What was the average pack size of this pack for the years represented in the data?

```r
anyNA(ynp$packsize_aug)
```

```
## [1] TRUE
```


```r
  mean(ynp$packsize_aug, na.rm=T)
```

```
## [1] 11.23868
```


Problem 8. (4 points) Pack dynamics can be hard to predict- even for strong packs like the Druid Peak pack. At which year did the Druid Peak pack have the largest pack size? What do you think happened in 2010?


```r
ynp %>% 
  filter(pack=="druid") %>% 
  select(biolyr, packsize_aug) %>% 
  group_by(biolyr) %>% 
  arrange(desc(packsize_aug))
```

```
## # A tibble: 15 × 2
## # Groups:   biolyr [15]
##    biolyr packsize_aug
##     <int>        <dbl>
##  1   2001           37
##  2   2000           27
##  3   2008           21
##  4   2003           18
##  5   2007           18
##  6   2002           16
##  7   2006           15
##  8   2004           13
##  9   2009           12
## 10   1999            9
## 11   1998            8
## 12   1997            5
## 13   1996            5
## 14   2005            5
## 15   2010            0
```


```r
ynp %>% 
  filter(pack=="druid") %>% 
  select(biolyr, packsize_aug) %>% 
  group_by(biolyr) %>% 
  arrange(desc(biolyr))
```

```
## # A tibble: 15 × 2
## # Groups:   biolyr [15]
##    biolyr packsize_aug
##     <int>        <dbl>
##  1   2010            0
##  2   2009           12
##  3   2008           21
##  4   2007           18
##  5   2006           15
##  6   2005            5
##  7   2004           13
##  8   2003           18
##  9   2002           16
## 10   2001           37
## 11   2000           27
## 12   1999            9
## 13   1998            8
## 14   1997            5
## 15   1996            5
```

In 2010, the Druid Peak wolf pack went extinct. The pack size was a mere 12 wolves in 2009. These wolves could have been killed due to hunters or possibly their habitat was destroyed. Another competing animal could have been introduced into the park, where competing for similar foods could have ruined their chances of being able to feed themselves. Since there are other wolf packs in the park, they could have been competing with one another, leading to the decline of the Druids Peak wolfpack.

Problem 9. (5 points) Among the YNP wolf packs, which one has had the highest overall persistence `persisty1` for the years represented in the data? Look this pack up online and tell me what is unique about its behavior- specifically, what prey animals does this pack specialize on?  


```r
ynp %>%
  select(pack, persisty1, biolyr) %>% 
  group_by(pack) %>%
  summarize(total_persistence = sum(persisty1)) %>%
  arrange(desc(total_persistence))  
```

```
## # A tibble: 46 × 2
##    pack        total_persistence
##    <chr>                   <int>
##  1 mollies                    26
##  2 cougar                     20
##  3 yelldelta                  18
##  4 leopold                    12
##  5 agate                      10
##  6 8mile                       9
##  7 canyon                      9
##  8 gibbon/mary                 9
##  9 junction                    8
## 10 lamar                       8
## # ℹ 36 more rows
```

The mollies wolf pack had the highest overall persistence amongst the years in the data. According to Google, this wolf pack preys on large animals, specifically elk and bison. This wolf pack was not only the first in Yellowstone to eat bison, but was also one of the longest lasting wolf packs at Yellowstone. What is unique about their behavior is that there are many strong "alpha-females". the carcasses from the bison they hunt are used to feed other animals in the park, including Grizzly Bears.


Problem 10. (3 points) Perform one analysis or exploration of your choice on the `wolves` data. Your answer needs to include at least two lines of code and not be a summary function.  



```r
wolves %>% 
  filter(pack=="Pinto") %>% 
  select(pack, biolyr, reprody1) %>% 
  arrange(desc(biolyr))
```

```
##    pack biolyr reprody1
## 1 Pinto   2007        0
## 2 Pinto   2006        1
```
For this last question, I was curious on if the Pinto pack had reproduced and wanted to arrange it by year. According to the wolves data, the Pinto pack only reproduced in the year 2007. Pup were observed in 2007 but not in 2006. 

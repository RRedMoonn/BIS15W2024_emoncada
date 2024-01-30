---
title: "Lab 4 Homework"
author: "Eva Moncada"
date: "2024-01-30"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv ("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
homerange
```

```
## # A tibble: 569 × 24
##    taxon        common.name class order family genus species primarymethod N    
##    <chr>        <chr>       <chr> <chr> <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake fishes  american e… acti… angu… angui… angu… rostra… telemetry     16   
##  2 river fishes blacktail … acti… cypr… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 river fishes central st… acti… cypr… cypri… camp… anomal… mark-recaptu… 20   
##  4 river fishes rosyside d… acti… cypr… cypri… clin… fundul… mark-recaptu… 26   
##  5 river fishes longnose d… acti… cypr… cypri… rhin… catara… mark-recaptu… 17   
##  6 river fishes muskellunge acti… esoc… esoci… esox  masqui… telemetry     5    
##  7 marine fish… pollack     acti… gadi… gadid… poll… pollac… telemetry     2    
##  8 marine fish… saithe      acti… gadi… gadid… poll… virens  telemetry     2    
##  9 marine fish… lined surg… acti… perc… acant… acan… lineat… direct obser… <NA> 
## 10 marine fish… orangespin… acti… perc… acant… naso  litura… telemetry     8    
## # ℹ 559 more rows
## # ℹ 15 more variables: mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <dbl>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
dim(homerange)
```

```
## [1] 569  24
```


```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
homerange$class
```

```
##   [1] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##   [5] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##   [9] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [13] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [17] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [21] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [25] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [29] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [33] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [37] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [41] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [45] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [49] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [53] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [57] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [61] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [65] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [69] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [73] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [77] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [81] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [85] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [89] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [93] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
##  [97] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
## [101] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
## [105] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
## [109] "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii"
## [113] "actinopterygii" "aves"           "aves"           "aves"          
## [117] "aves"           "aves"           "aves"           "aves"          
## [121] "aves"           "aves"           "aves"           "aves"          
## [125] "aves"           "aves"           "aves"           "aves"          
## [129] "aves"           "aves"           "aves"           "aves"          
## [133] "aves"           "aves"           "aves"           "aves"          
## [137] "aves"           "aves"           "aves"           "aves"          
## [141] "aves"           "aves"           "aves"           "aves"          
## [145] "aves"           "aves"           "aves"           "aves"          
## [149] "aves"           "aves"           "aves"           "aves"          
## [153] "aves"           "aves"           "aves"           "aves"          
## [157] "aves"           "aves"           "aves"           "aves"          
## [161] "aves"           "aves"           "aves"           "aves"          
## [165] "aves"           "aves"           "aves"           "aves"          
## [169] "aves"           "aves"           "aves"           "aves"          
## [173] "aves"           "aves"           "aves"           "aves"          
## [177] "aves"           "aves"           "aves"           "aves"          
## [181] "aves"           "aves"           "aves"           "aves"          
## [185] "aves"           "aves"           "aves"           "aves"          
## [189] "aves"           "aves"           "aves"           "aves"          
## [193] "aves"           "aves"           "aves"           "aves"          
## [197] "aves"           "aves"           "aves"           "aves"          
## [201] "aves"           "aves"           "aves"           "aves"          
## [205] "aves"           "aves"           "aves"           "aves"          
## [209] "aves"           "aves"           "aves"           "aves"          
## [213] "aves"           "aves"           "aves"           "aves"          
## [217] "aves"           "aves"           "aves"           "aves"          
## [221] "aves"           "aves"           "aves"           "aves"          
## [225] "aves"           "aves"           "aves"           "aves"          
## [229] "aves"           "aves"           "aves"           "aves"          
## [233] "aves"           "aves"           "aves"           "aves"          
## [237] "aves"           "aves"           "aves"           "aves"          
## [241] "aves"           "aves"           "aves"           "aves"          
## [245] "aves"           "aves"           "aves"           "aves"          
## [249] "aves"           "aves"           "aves"           "aves"          
## [253] "aves"           "mammalia"       "mammalia"       "mammalia"      
## [257] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [261] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [265] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [269] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [273] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [277] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [281] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [285] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [289] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [293] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [297] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [301] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [305] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [309] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [313] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [317] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [321] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [325] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [329] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [333] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [337] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [341] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [345] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [349] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [353] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [357] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [361] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [365] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [369] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [373] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [377] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [381] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [385] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [389] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [393] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [397] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [401] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [405] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [409] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [413] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [417] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [421] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [425] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [429] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [433] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [437] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [441] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [445] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [449] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [453] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [457] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [461] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [465] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [469] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [473] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [477] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [481] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [485] "mammalia"       "mammalia"       "mammalia"       "mammalia"      
## [489] "mammalia"       "mammalia"       "mammalia"       "reptilia"      
## [493] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [497] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [501] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [505] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [509] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [513] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [517] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [521] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [525] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [529] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [533] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [537] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [541] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [545] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [549] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [553] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [557] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [561] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [565] "reptilia"       "reptilia"       "reptilia"       "reptilia"      
## [569] "reptilia"
```


```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)
```


```r
homerange$taxon
```

```
##   [1] lake fishes   river fishes  river fishes  river fishes  river fishes 
##   [6] river fishes  marine fishes marine fishes marine fishes marine fishes
##  [11] marine fishes marine fishes marine fishes lake fishes   lake fishes  
##  [16] lake fishes   river fishes  river fishes  lake fishes   lake fishes  
##  [21] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [26] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [31] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [36] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [41] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [46] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [51] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [56] marine fishes marine fishes marine fishes marine fishes lake fishes  
##  [61] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [66] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [71] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [76] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [81] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [86] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [91] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [96] marine fishes river fishes  river fishes  river fishes  river fishes 
## [101] lake fishes   river fishes  river fishes  river fishes  marine fishes
## [106] marine fishes marine fishes marine fishes marine fishes lake fishes  
## [111] marine fishes marine fishes marine fishes birds         birds        
## [116] birds         birds         birds         birds         birds        
## [121] birds         birds         birds         birds         birds        
## [126] birds         birds         birds         birds         birds        
## [131] birds         birds         birds         birds         birds        
## [136] birds         birds         birds         birds         birds        
## [141] birds         birds         birds         birds         birds        
## [146] birds         birds         birds         birds         birds        
## [151] birds         birds         birds         birds         birds        
## [156] birds         birds         birds         birds         birds        
## [161] birds         birds         birds         birds         birds        
## [166] birds         birds         birds         birds         birds        
## [171] birds         birds         birds         birds         birds        
## [176] birds         birds         birds         birds         birds        
## [181] birds         birds         birds         birds         birds        
## [186] birds         birds         birds         birds         birds        
## [191] birds         birds         birds         birds         birds        
## [196] birds         birds         birds         birds         birds        
## [201] birds         birds         birds         birds         birds        
## [206] birds         birds         birds         birds         birds        
## [211] birds         birds         birds         birds         birds        
## [216] birds         birds         birds         birds         birds        
## [221] birds         birds         birds         birds         birds        
## [226] birds         birds         birds         birds         birds        
## [231] birds         birds         birds         birds         birds        
## [236] birds         birds         birds         birds         birds        
## [241] birds         birds         birds         birds         birds        
## [246] birds         birds         birds         birds         birds        
## [251] birds         birds         birds         mammals       mammals      
## [256] mammals       mammals       mammals       mammals       mammals      
## [261] mammals       mammals       mammals       mammals       mammals      
## [266] mammals       mammals       mammals       mammals       mammals      
## [271] mammals       mammals       mammals       mammals       mammals      
## [276] mammals       mammals       mammals       mammals       mammals      
## [281] mammals       mammals       mammals       mammals       mammals      
## [286] mammals       mammals       mammals       mammals       mammals      
## [291] mammals       mammals       mammals       mammals       mammals      
## [296] mammals       mammals       mammals       mammals       mammals      
## [301] mammals       mammals       mammals       mammals       mammals      
## [306] mammals       mammals       mammals       mammals       mammals      
## [311] mammals       mammals       mammals       mammals       mammals      
## [316] mammals       mammals       mammals       mammals       mammals      
## [321] mammals       mammals       mammals       mammals       mammals      
## [326] mammals       mammals       mammals       mammals       mammals      
## [331] mammals       mammals       mammals       mammals       mammals      
## [336] mammals       mammals       mammals       mammals       mammals      
## [341] mammals       mammals       mammals       mammals       mammals      
## [346] mammals       mammals       mammals       mammals       mammals      
## [351] mammals       mammals       mammals       mammals       mammals      
## [356] mammals       mammals       mammals       mammals       mammals      
## [361] mammals       mammals       mammals       mammals       mammals      
## [366] mammals       mammals       mammals       mammals       mammals      
## [371] mammals       mammals       mammals       mammals       mammals      
## [376] mammals       mammals       mammals       mammals       mammals      
## [381] mammals       mammals       mammals       mammals       mammals      
## [386] mammals       mammals       mammals       mammals       mammals      
## [391] mammals       mammals       mammals       mammals       mammals      
## [396] mammals       mammals       mammals       mammals       mammals      
## [401] mammals       mammals       mammals       mammals       mammals      
## [406] mammals       mammals       mammals       mammals       mammals      
## [411] mammals       mammals       mammals       mammals       mammals      
## [416] mammals       mammals       mammals       mammals       mammals      
## [421] mammals       mammals       mammals       mammals       mammals      
## [426] mammals       mammals       mammals       mammals       mammals      
## [431] mammals       mammals       mammals       mammals       mammals      
## [436] mammals       mammals       mammals       mammals       mammals      
## [441] mammals       mammals       mammals       mammals       mammals      
## [446] mammals       mammals       mammals       mammals       mammals      
## [451] mammals       mammals       mammals       mammals       mammals      
## [456] mammals       mammals       mammals       mammals       mammals      
## [461] mammals       mammals       mammals       mammals       mammals      
## [466] mammals       mammals       mammals       mammals       mammals      
## [471] mammals       mammals       mammals       mammals       mammals      
## [476] mammals       mammals       mammals       mammals       mammals      
## [481] mammals       mammals       mammals       mammals       mammals      
## [486] mammals       mammals       mammals       mammals       mammals      
## [491] mammals       lizards       snakes        snakes        snakes       
## [496] snakes        snakes        snakes        snakes        snakes       
## [501] snakes        snakes        snakes        snakes        snakes       
## [506] snakes        snakes        snakes        snakes        snakes       
## [511] snakes        snakes        snakes        snakes        snakes       
## [516] snakes        snakes        lizards       lizards       lizards      
## [521] lizards       lizards       lizards       lizards       lizards      
## [526] lizards       snakes        lizards       snakes        snakes       
## [531] snakes        snakes        snakes        snakes        snakes       
## [536] snakes        snakes        snakes        snakes        snakes       
## [541] snakes        snakes        snakes        turtles       turtles      
## [546] turtles       turtles       turtles       turtles       turtles      
## [551] turtles       turtles       turtles       turtles       turtles      
## [556] turtles       tortoises     tortoises     tortoises     tortoises    
## [561] tortoises     tortoises     tortoises     tortoises     tortoises    
## [566] tortoises     tortoises     tortoises     turtles      
## 9 Levels: birds lake fishes lizards mammals marine fishes ... turtles
```


**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

#Changing some of the names since they incorrectly written. 


```r
colnames(homerange) <- c("taxon", "common_name", "class", "order", "family", "genus", "species", "primary_method", "N", "mean_mass_g", "log10_mass", "alternative_mass_reference", "mean_hra_m2", "log10_hra", "hra_reference", "realm", "thermoregulation", "locomotion", "trophic_guild", "dimension", "prey_mass", "log10_prey_mass", "PPMR", "prey_size_reference")
```



```r
taxa <- homerange[, c("taxon", "common_name", "class", "order", "family", "genus", "species")]
head(taxa)
```

```
## # A tibble: 6 × 7
##   taxon        common_name         class          order     family genus species
##   <fct>        <chr>               <chr>          <fct>     <chr>  <chr> <chr>  
## 1 lake fishes  american eel        actinopterygii anguilli… angui… angu… rostra…
## 2 river fishes blacktail redhorse  actinopterygii cyprinif… catos… moxo… poecil…
## 3 river fishes central stoneroller actinopterygii cyprinif… cypri… camp… anomal…
## 4 river fishes rosyside dace       actinopterygii cyprinif… cypri… clin… fundul…
## 5 river fishes longnose dace       actinopterygii cyprinif… cypri… rhin… catara…
## 6 river fishes muskellunge         actinopterygii esocifor… esoci… esox  masqui…
```

**5. The variable `taxon` identifies the common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic_guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  


```r
carnivores <- filter(homerange, trophic_guild == "carnivore")
herbivores <- filter(homerange, trophic_guild == "herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
anyNA(carnivores$mean_hra_m2)
```

```
## [1] FALSE
```


```r
mean(carnivores$mean_hra_m2, na.rm =T)
```

```
## [1] 13039918
```



```r
anyNA(herbivores$mean_hra_m2)
```

```
## [1] FALSE
```


```r
mean(herbivores$mean_hra_m2, na.rm =T)
```

```
## [1] 34137012
```


**9. Make a new dataframe `owls` that is limited to the mean mass, log10 mass, family, genus, and species of owls in the database. Which is the smallest owl? What is its common name? Do a little bit of searching online to see what you can learn about this species and provide a link below** 


```r
homerange$order
```

```
##   [1] anguilliformes        cypriniformes         cypriniformes        
##   [4] cypriniformes         cypriniformes         esociformes          
##   [7] gadiformes            gadiformes            perciformes          
##  [10] perciformes           perciformes           perciformes          
##  [13] perciformes           perciformes           perciformes          
##  [16] perciformes           perciformes           perciformes          
##  [19] perciformes           perciformes           perciformes          
##  [22] perciformes           perciformes           perciformes          
##  [25] perciformes           perciformes           perciformes          
##  [28] perciformes           perciformes           perciformes          
##  [31] perciformes           perciformes           perciformes          
##  [34] perciformes           perciformes           perciformes          
##  [37] perciformes           perciformes           perciformes          
##  [40] perciformes           perciformes           perciformes          
##  [43] perciformes           perciformes           perciformes          
##  [46] perciformes           perciformes           perciformes          
##  [49] perciformes           perciformes           perciformes          
##  [52] perciformes           perciformes           perciformes          
##  [55] perciformes           perciformes           perciformes          
##  [58] perciformes           perciformes           perciformes          
##  [61] perciformes           perciformes           perciformes          
##  [64] perciformes           perciformes           perciformes          
##  [67] perciformes           perciformes           perciformes          
##  [70] perciformes           perciformes           perciformes          
##  [73] perciformes           perciformes           perciformes          
##  [76] perciformes           perciformes           perciformes          
##  [79] perciformes           perciformes           perciformes          
##  [82] perciformes           perciformes           perciformes          
##  [85] perciformes           perciformes           perciformes          
##  [88] perciformes           perciformes           perciformes          
##  [91] perciformes           perciformes           perciformes          
##  [94] perciformes           perciformes           perciformes          
##  [97] salmoniformes         salmoniformes         salmoniformes        
## [100] salmoniformes         salmoniformes         scorpaeniformes      
## [103] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [106] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [109] scorpaeniformes       siluriformes          syngnathiformes      
## [112] syngnathiformes       tetraodontiformes\xa0 accipitriformes      
## [115] accipitriformes       accipitriformes       accipitriformes      
## [118] accipitriformes       accipitriformes       anseriformes         
## [121] apterygiformes        caprimulgiformes      charadriiformes      
## [124] columbidormes         columbiformes         columbiformes        
## [127] coraciiformes         coraciiformes         cuculiformes         
## [130] cuculiformes          cuculiformes          cuculiformes         
## [133] falconiformes         falconiformes         falconiformes        
## [136] falconiformes         falconiformes         falconiformes        
## [139] falconiformes         falconiformes         falconiformes        
## [142] falconiformes         falconiformes         falconiformes        
## [145] falconiformes         falconiformes         falconiformes        
## [148] falconiformes         falconiformes         galliformes          
## [151] galliformes           galliformes           galliformes          
## [154] galliformes           galliformes           galliformes          
## [157] galliformes           gruiformes            gruiformes           
## [160] gruiformes            passeriformes         passeriformes        
## [163] passeriformes         passeriformes         passeriformes        
## [166] passeriformes         passeriformes         passeriformes        
## [169] passeriformes         passeriformes         passeriformes        
## [172] passeriformes         passeriformes         passeriformes        
## [175] passeriformes         passeriformes         passeriformes        
## [178] passeriformes         passeriformes         passeriformes        
## [181] passeriformes         passeriformes         passeriformes        
## [184] passeriformes         passeriformes         passeriformes        
## [187] passeriformes         passeriformes         passeriformes        
## [190] passeriformes         passeriformes         passeriformes        
## [193] passeriformes         passeriformes         passeriformes        
## [196] passeriformes         passeriformes         passeriformes        
## [199] passeriformes         passeriformes         passeriformes        
## [202] passeriformes         passeriformes         passeriformes        
## [205] passeriformes         passeriformes         passeriformes        
## [208] passeriformes         passeriformes         passeriformes        
## [211] passeriformes         passeriformes         passeriformes        
## [214] passeriformes         passeriformes         passeriformes        
## [217] passeriformes         passeriformes         passeriformes        
## [220] passeriformes         passeriformes         passeriformes        
## [223] passeriformes         passeriformes         passeriformes        
## [226] passeriformes         passeriformes         passeriformes        
## [229] passeriformes         passeriformes         pelecaniformes       
## [232] pelecaniformes        piciformes            piciformes           
## [235] piciformes            piciformes            piciformes           
## [238] piciformes            piciformes            psittaciformes       
## [241] rheiformes            rheiformes            strigiformes         
## [244] strigiformes          strigiformes          strigiformes         
## [247] strigiformes          strigiformes          strigiformes         
## [250] strigiformes          strigiformes          struthioniformes     
## [253] tinamiformes          afrosoricida          afrosoricida         
## [256] artiodactyla          artiodactyla          artiodactyla         
## [259] artiodactyla          artiodactyla          artiodactyla         
## [262] artiodactyla          artiodactyla          artiodactyla         
## [265] artiodactyla          artiodactyla          artiodactyla         
## [268] artiodactyla          artiodactyla          artiodactyla         
## [271] artiodactyla          artiodactyla          artiodactyla         
## [274] artiodactyla          artiodactyla          artiodactyla         
## [277] artiodactyla          artiodactyla          artiodactyla         
## [280] artiodactyla          artiodactyla          artiodactyla         
## [283] artiodactyla          artiodactyla          artiodactyla         
## [286] artiodactyla          artiodactyla          artiodactyla         
## [289] artiodactyla          artiodactyla          artiodactyla         
## [292] artiodactyla          artiodactyla          artiodactyla         
## [295] carnivora             carnivora             carnivora            
## [298] carnivora             carnivora             carnivora            
## [301] carnivora             carnivora             carnivora            
## [304] carnivora             carnivora             carnivora            
## [307] carnivora             carnivora             carnivora            
## [310] carnivora             carnivora             carnivora            
## [313] carnivora             carnivora             carnivora            
## [316] carnivora             carnivora             carnivora            
## [319] carnivora             carnivora             carnivora            
## [322] carnivora             carnivora             carnivora            
## [325] carnivora             carnivora             carnivora            
## [328] carnivora             carnivora             carnivora            
## [331] carnivora             carnivora             carnivora            
## [334] carnivora             carnivora             carnivora            
## [337] carnivora             carnivora             carnivora            
## [340] carnivora             carnivora             carnivora            
## [343] carnivora             carnivora             carnivora            
## [346] carnivora             carnivora             carnivora            
## [349] carnivora             carnivora             dasyuromorpha        
## [352] dasyuromorpha         dasyuromorpha         dasyuromorpia        
## [355] didelphimorphia       didelphimorphia       diprodontia          
## [358] diprodontia           diprodontia           diprodontia          
## [361] diprodontia           diprodontia           diprodontia          
## [364] diprodontia           diprodontia           diprodontia          
## [367] diprodontia           diprodontia           diprotodontia        
## [370] diprotodontia         diprotodontia         diprotodontia        
## [373] diprotodontia         diprotodontia         diprotodontia        
## [376] erinaceomorpha        erinaceomorpha        lagomorpha           
## [379] lagomorpha            lagomorpha            lagomorpha           
## [382] lagomorpha            lagomorpha            lagomorpha           
## [385] lagomorpha            lagomorpha            lagomorpha           
## [388] lagomorpha            lagomorpha            lagomorpha           
## [391] lagomorpha            macroscelidea         macroscelidea        
## [394] macroscelidea         monotrematae          peramelemorphia      
## [397] peramelemorphia       perissodactyla        perissodactyla       
## [400] perissodactyla        pilosa                proboscidea          
## [403] proboscidea           roden                 rodentia             
## [406] rodentia              rodentia              rodentia             
## [409] rodentia              rodentia              rodentia             
## [412] rodentia              rodentia              rodentia             
## [415] rodentia              rodentia              rodentia             
## [418] rodentia              rodentia              rodentia             
## [421] rodentia              rodentia              rodentia             
## [424] rodentia              rodentia              rodentia             
## [427] rodentia              rodentia              rodentia             
## [430] rodentia              rodentia              rodentia             
## [433] rodentia              rodentia              rodentia             
## [436] rodentia              rodentia              rodentia             
## [439] rodentia              rodentia              rodentia             
## [442] rodentia              rodentia              rodentia             
## [445] rodentia              rodentia              rodentia             
## [448] rodentia              rodentia              rodentia             
## [451] rodentia              rodentia              rodentia             
## [454] rodentia              rodentia              rodentia             
## [457] rodentia              rodentia              rodentia             
## [460] rodentia              rodentia              rodentia             
## [463] rodentia              rodentia              rodentia             
## [466] rodentia              rodentia              rodentia             
## [469] rodentia              rodentia              rodentia             
## [472] rodentia              rodentia              rodentia             
## [475] rodentia              rodentia              rodentia             
## [478] rodentia              rodentia              rodentia             
## [481] rodentia              soricomorpha          soricomorpha         
## [484] soricomorpha          soricomorpha          soricomorpha         
## [487] soricomorpha          soricomorpha          soricomorpha         
## [490] soricomorpha          soricomorpha          squamata             
## [493] squamata              squamata              squamata             
## [496] squamata              squamata              squamata             
## [499] squamata              squamata              squamata             
## [502] squamata              squamata              squamata             
## [505] squamata              squamata              squamata             
## [508] squamata              squamata              squamata             
## [511] squamata              squamata              squamata             
## [514] squamata              squamata              squamata             
## [517] squamata              squamata              squamata             
## [520] squamata              squamata              squamata             
## [523] squamata              squamata              squamata             
## [526] squamata              squamata              squamata             
## [529] squamata              squamata              squamata             
## [532] squamata              squamata              squamata             
## [535] squamata              squamata              squamata             
## [538] squamata              squamata              squamata             
## [541] squamata              squamata              squamata             
## [544] testudines            testudines            testudines           
## [547] testudines            testudines            testudines           
## [550] testudines            testudines            testudines           
## [553] testudines            testudines            testudines           
## [556] testudines            testudines            testudines           
## [559] testudines            testudines            testudines           
## [562] testudines            testudines            testudines           
## [565] testudines            testudines            testudines           
## [568] testudines            testudines           
## 51 Levels: accipitriformes afrosoricida anguilliformes ... tetraodontiformes\xa0
```


```r
homerange %>% 
  select(taxon, order, mean_mass_g, log10_mass, family, genus, species) %>% 
  filter(taxon=="birds", order== "strigiformes") %>% 
  arrange(desc(mean_mass_g))
```

```
## # A tibble: 9 × 7
##   taxon order        mean_mass_g log10_mass family    genus      species    
##   <fct> <fct>              <dbl>      <dbl> <chr>     <chr>      <chr>      
## 1 birds strigiformes      2191         3.34 strigidae bubo       bubo       
## 2 birds strigiformes      1920         3.28 strigidae nyctea     scandiaca  
## 3 birds strigiformes      1510         3.18 strigidae bubo       virginianus
## 4 birds strigiformes       519         2.72 strigidae strix      aluco      
## 5 birds strigiformes       285         2.45 tytonidae tyto       alba       
## 6 birds strigiformes       252         2.40 strigidae asio       otus       
## 7 birds strigiformes       156.        2.19 strigidae athene     noctua     
## 8 birds strigiformes       119         2.08 strigidae aegolius   funereus   
## 9 birds strigiformes        61.3       1.79 strigidae glaucidium passerinum
```
The smallest owl is species passerinum from the glaucidium, genus family (Glaucidium passerinum). This  owl is the smallest in Europe with a wingspan of 32-39 centimeters and weight of only 47-83 grams,which is equivalent to around 0.10-0.18 pounds. This owl is also found in areas of Asia including Mongolia and China. This species lives in coniferous forests and mountainous areas. These owls do not migrate and hence hoard their carnivorous foods in the autumn to be consumed in the winter. Their carnivorous diet primarily consists of small mammals, small birds, lizards, fish and insects. 

Source: https://animalia.bio/eurasian-pygmy-owl?letter=e

**10. As measured by the data, which bird species has the largest homerange? Show all of your work, please. Look this species up online and tell me about it!**.  

```r
homerange %>% 
  arrange(desc(mean_hra_m2)) %>% 
  filter(class == "aves")
```

```
## # A tibble: 140 × 24
##    taxon common_name       class order family genus species primary_method N    
##    <fct> <chr>             <chr> <fct> <chr>  <chr> <chr>   <chr>          <chr>
##  1 birds caracara          aves  falc… falco… cara… cheriw… telemetry      26   
##  2 birds Montagu's harrier aves  falc… accip… circ… pygarg… telemetry*     <NA> 
##  3 birds peregrine falcon  aves  falc… falco… falco peregr… telemetry*     <NA> 
##  4 birds booted eagle      aves  acci… accip… hier… pennat… telemetry      4    
##  5 birds ostrich           aves  stru… strut… stru… camelus telemetry      1    
##  6 birds short-toed snake… aves  acci… accip… circ… gallic… telemetry*     <NA> 
##  7 birds European turtle … aves  colu… colum… stre… turtur  telemetry*     <NA> 
##  8 birds Egyptian vulture  aves  acci… accip… neop… percno… telemetry*     <NA> 
##  9 birds common buzzard    aves  acci… accip… buteo buteo   telemetry*     <NA> 
## 10 birds lanner falcon     aves  falc… falco… falco biarmi… telemetry*     <NA> 
## # ℹ 130 more rows
## # ℹ 15 more variables: mean_mass_g <dbl>, log10_mass <dbl>,
## #   alternative_mass_reference <chr>, mean_hra_m2 <dbl>, log10_hra <dbl>,
## #   hra_reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic_guild <chr>, dimension <dbl>, prey_mass <dbl>,
## #   log10_prey_mass <dbl>, PPMR <dbl>, prey_size_reference <chr>
```
The cheriway species, or Caracara, has the largest homerange. The Crested Caracara are omnivorous falcons that primarily live in Central and Southern Americas, along with some southern states in the United States. These birds are black and white with yellow-orange skin on their legs and around their bills.They are medium sized with their wingspan of 122-125 centimeters and lengths of 49-58 centimeters. This species is the only falcon that build their own nests while other falcons use old nests created by other species. 

Source: https://www.allaboutbirds.org/guide/Crested_Caracara/overview 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   

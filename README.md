Project 2 F Stat 558
================
Cartron and Rao
9/30/2022

API code

``` r
library(httr)
mydata<-GET("https://api.spoonacular.com/recipes/complexSearch?query=pasta&maxFat=25&number=2&apiKey=55fcdcfd9f374fa3adb1246f5c30c78b")
library(dplyr)
library(jsonlite)
parsed <- fromJSON(rawToChar(mydata$content))
str(parsed, max.level = 1)
```

    ## List of 4
    ##  $ results     :'data.frame':    2 obs. of  5 variables:
    ##  $ offset      : int 0
    ##  $ number      : int 2
    ##  $ totalResults: int 127

``` r
parsed$results %>%
  colnames()
```

    ## [1] "id"        "title"     "image"     "imageType" "nutrition"

``` r
parsed$results$title[2] 
```

    ## [1] "Pasta and Seafood"

Project 2 F Stat 558
================
Cartron and Rao
9/30/2022

API code sample structure

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

Now let’s create custom functions to call in data from the API.

``` r
get_recipe <- function(key, query, maxCarbs, minCarbs) {

param_list <- list(apiKey = key, query = NULL, maxCarbs = maxCarbs, minCarbs = minCarbs) 
  
base_url <- "https://api.spoonacular.com/recipes/complexSearch"
recipe_dat <- GET(paste(base_url), query = param_list)

parsed <- fromJSON(rawToChar(recipe_dat$content), flatten = TRUE)

return(parsed)
  
}
  

#Below was what inspired the function above. Still some issues to work out. 
recipes <- GET("https://api.spoonacular.com/recipes/complexSearch?apiKey=e565b5df568f4b3fa1f5a044377e989a")
df_recipe_initial <- jsonlite::fromJSON(rawToChar(recipe_nutrition$content), flatten = TRUE)

df_recipe <- df_recipe_initial$results
df_recipe
```

    ##        id                                             title                                                   image
    ## 1  716426 Cauliflower, Brown Rice, and Vegetable Fried Rice https://spoonacular.com/recipeImages/716426-312x231.jpg
    ## 2  715594            Homemade Garlic and Basil French Fries https://spoonacular.com/recipeImages/715594-312x231.jpg
    ## 3  715497                   Berry Banana Breakfast Smoothie https://spoonacular.com/recipeImages/715497-312x231.jpg
    ## 4  644387                                     Garlicky Kale https://spoonacular.com/recipeImages/644387-312x231.jpg
    ## 5  716268                       African Chicken Peanut Stew https://spoonacular.com/recipeImages/716268-312x231.jpg
    ## 6  716381                               Nigerian Snail Stew https://spoonacular.com/recipeImages/716381-312x231.jpg
    ## 7  782601                         Red Kidney Bean Jambalaya https://spoonacular.com/recipeImages/782601-312x231.jpg
    ## 8  794349                  Broccoli and Chickpea Rice Salad https://spoonacular.com/recipeImages/794349-312x231.jpg
    ## 9  715446                             Slow Cooker Beef Stew https://spoonacular.com/recipeImages/715446-312x231.jpg
    ## 10 715415          Red Lentil Soup with Chicken and Turnips https://spoonacular.com/recipeImages/715415-312x231.jpg
    ##    imageType
    ## 1        jpg
    ## 2        jpg
    ## 3        jpg
    ## 4        jpg
    ## 5        jpg
    ## 6        jpg
    ## 7        jpg
    ## 8        jpg
    ## 9        jpg
    ## 10       jpg

``` r
#get_recipe(e565b5df568f4b3fa1f5a044377e989a, 1000, 200)
```

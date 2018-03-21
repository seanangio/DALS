---
title: "Probability Distributions Exercises"
author: "Sean Angiolillo"
date: "8 March 2018"
output: 
  html_document: 
    keep_md: yes
---



In the video you just watched, Rafa looked at distributions of heights, and asked what was the probability of someone being shorter than a given height. In this assessment, we are going to ask the same question, but instead of people and heights, we are going to look at whole countries and the average life expectancy in those countries.

We will use the data set called "Gapminder" which is available as an R-package on Github. This data set contains the life expectancy, GDP per capita, and population by country, every five years, from 1952 to 2007. It is an excerpt of a larger and more comprehensive set of data available on Gapminder.org, and the R package of this dataset was created by the statistics professor Jennifer Bryan.

First, install the gapminder data using:


```r
if ("gapminder" %in% rownames(installed.packages()) == FALSE) {
    install.packages("gapminder")
}
```

Next, load the gapminder data set. To find out more information about the data set, use ?gapminder which will bring up a help file. To return the first few lines of the data set, use the function head().


```r
library(gapminder)
data(gapminder)
head(gapminder)
```

```
## # A tibble: 6 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
## 4 Afghanistan Asia       1967    34.0 11537966      836.
## 5 Afghanistan Asia       1972    36.1 13079460      740.
## 6 Afghanistan Asia       1977    38.4 14880372      786.
```

Create a vector 'x' of the life expectancies of each country for the year 1952. Plot a histogram of these life expectancies to see the spread of the different countries.


```r
library(dplyr)
x <- gapminder %>% filter(year == 1952) %>% select(lifeExp) %>% unlist
hist(x)
```

![](probability_distributions_exercises_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


## Probability Distributions Exercises #1

In statistics, the empirical cumulative distribution function (or empirical cdf or empirical distribution function) is the function F(a) for any a, which tells you the proportion of the values which are less than or equal to a.

We can compute F in two ways: the simplest way is to type mean(x <= a). This calculates the number of values in x which are less than or equal a, divided by the total number of values in x, in other words the proportion of values less than or equal to a.

The second way, which is a bit more complex for beginners, is to use the ecdf() function. This is a bit complicated because this is a function that doesn't return a value, but a function.

Let's continue, using the simpler, mean() function.

What is the proportion of countries in 1952 that have a life expectancy less than or equal to 40?


```r
mean(x <= 40)
```

```
## [1] 0.2887324
```

 
## Probability Distributions Exercises #2

What is the proportion of countries in 1952 that have a life expectancy between 40 and 60 years? Hint: this is the proportion that have a life expectancy less than or equal to 60 years, minus the proportion that have a life expectancy less than or equal to 40 years.


```r
mean(x <= 60) - mean(x <= 40)
```

```
## [1] 0.4647887
```

```r
mean(x < 60 & x > 40)
```

```
## [1] 0.4647887
```

### sapply() on a custom function
Suppose we want to plot the proportions of countries with life expectancy 'q' for a range of different years. R has a built in function for this, plot(ecdf(x)), but suppose we didn't know this. The function is quite easy to build, by turning the code from question 1.1 into a custom function, and then using sapply(). Our custom function will take an input variable 'q', and return the proportion of countries in 'x' less than or equal to q. The curly brackets { and }, allow us to write an R function which spans multiple lines:


```r
prop = function(q) {
  mean(x <= q)
}
```

Try this out for a value of 'q':  prop(40)


```r
prop(40)
```

```
## [1] 0.2887324
```


Now let's build a range of q's that we can apply the function to:


```r
qs = seq(from=min(x), to=max(x), length=20)
qs
```

```
##  [1] 28.80100 31.10989 33.41879 35.72768 38.03658 40.34547 42.65437
##  [8] 44.96326 47.27216 49.58105 51.88995 54.19884 56.50774 58.81663
## [15] 61.12553 63.43442 65.74332 68.05221 70.36111 72.67000
```

Print 'qs' to the R console to see what the seq() function gave us. Now we can use sapply() to apply the 'prop' function to each element of 'qs':


```r
props = sapply(qs, prop)
props
```

```
##  [1] 0.007042254 0.028169014 0.063380282 0.105633803 0.204225352
##  [6] 0.288732394 0.408450704 0.492957746 0.535211268 0.577464789
## [11] 0.626760563 0.640845070 0.683098592 0.718309859 0.774647887
## [16] 0.809859155 0.852112676 0.922535211 0.964788732 1.000000000
```

Take a look at 'props', either by printing to the console, or by plotting it over qs:


```r
plot(qs, props)
```

![](probability_distributions_exercises_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

Note that we could also have written this in one line, by defining the 'prop' function but without naming it:


```r
props = sapply(qs, function(q) mean(x <= q))
```

This last style is called using an "inline" function or an "anonymous" function. Let's compare our homemade plot with the pre-built one in R:


```r
plot(ecdf(x))
```

![](probability_distributions_exercises_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

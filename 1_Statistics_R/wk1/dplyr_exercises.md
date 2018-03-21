---
title: "dplyr exercises"
author: "Sean Angiolillo"
date: "7 March 2018"
output: 
  html_document: 
    keep_md: yes
---



For these exercises, we will use a new dataset related to mammalian sleep. This link describes the data. Download the CSV file from this location:


```r
library(downloader)
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/msleep_ggplot2.csv"
filename <- basename(url)
if (!file.exists(filename)) download(url,destfile = filename)
```


## dplyr Exercises #1

Read in the `msleep_ggplot2.csv` file with the function `read.csv` and use the function `class` to determine what type of object is returned.


```r
dat <- read.csv("msleep_ggplot2.csv")
class(dat)
```

```
## [1] "data.frame"
```

## dplyr Exercises #2

Now use the filter function to select only the primates. How many animals in the table are primates? Hint: the nrow function gives you the number of rows of a data frame or matrix.


```r
library(dplyr)
dat %>%
    filter(order == "Primates") %>%
    nrow()
```

```
## [1] 12
```

## dplyr Exercises #3

What is the class of the object you obtain after subsetting the table to only include primates?


```r
primates <- dat %>% filter(order == "Primates")
class(primates)
```

```
## [1] "data.frame"
```

## dplyr Exercises #4

Now use the `select` function to extract the sleep (total) for the primates. What class is this object? Hint: use `%>%` to pipe the results of the filter function to select.


```r
primate_sleep_total <- primates %>% select(sleep_total)
class(primate_sleep_total)
```

```
## [1] "data.frame"
```


## dplyr Exercises #5

Now we want to calculate the average amount of sleep for primates (the average of the numbers computed above). One challenge is that the mean function requires a vector so, if we simply apply it to the output above, we get an error. Look at the help file for unlist and use it to compute the desired average.


```r
mean(unlist(primate_sleep_total))
```

```
## [1] 10.5
```


## dplyr Exercises #6

For the last exercise, we could also use the dplyr `summarize` function. We have not introduced this function, but you can read the help file and repeat exercise 5, this time using just filter and summarize to get the answer.


```r
primate_sleep_total %>% summarize(mean(sleep_total))
```

```
##   mean(sleep_total)
## 1              10.5
```


 

---
title: "Getting Started Exercises"
author: "Sean Angiolillo"
date: "7 March 2018"
output: 
  html_document: 
    keep_md: yes
---



Here we will test some of the basics of R data manipulation which you should know or should have learned by following the tutorials above. You will need to have the file femaleMiceWeights.csv in your working directory. As we showed above, one way to do this is by using the downloader package:

```r
library(downloader) 
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/femaleMiceWeights.csv"
filename <- "femaleMiceWeights.csv" 
if (!file.exists(filename)) download(url,destfile = filename)
```

## Getting Started Exercises #1

Read in the file femaleMiceWeights.csv and report the exact name of the column containing the weights.


```r
dat <- read.csv("femaleMiceWeights.csv")
names(dat)
```

```
## [1] "Diet"       "Bodyweight"
```

## Getting Started Exercises #2

The [ and ] symbols can be used to extract specific rows and specific columns of the table. What is the entry in the 12th row and second column?


```r
dat[12,2]
```

```
## [1] 26.25
```

## Getting Started Exercises #3

You should have learned how to use the \$ character to extract a column from a table and return it as a vector. Use \$ to extract the weight column and report the weight of the mouse in the 11th row.


```r
dat$Bodyweight[11]
```

```
## [1] 26.91
```

## Getting Started Exercises #4

The length function returns the number of elements in a vector. How many mice are included in our dataset?


```r
length(dat$Bodyweight)
```

```
## [1] 24
```

```r
#nrow(dat)
```

## Getting Started Exercises #5

To create a vector with the numbers 3 to 7, we can use seq(3,7) or, because they are consecutive, 3:7. View the data and determine what rows are associated with the high fat or hf diet. Then use the mean function to compute the average weight of these mice.


```r
mean(dat$Bodyweight[which(dat$Diet == "hf")])
```

```
## [1] 26.83417
```


## Getting Started Exercises #6

One of the functions we will be using often is sample. Read the help file for sample using ?sample. Now take a random sample of size 1 from the numbers 13 to 24 and report back the weight of the mouse represented by that row. Make sure to type set.seed(1) to ensure that everybody gets the same answer.


```r
set.seed(1)
dat[sample(13:24, 1),]$Bodyweight
```

```
## [1] 25.34
```


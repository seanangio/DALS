---
title: "Population, Samples, and Estimates Exercises"
author: "Sean Angiolillo"
date: "8 March 2018"
output: 
  html_document: 
    keep_md: yes
---



For these exercises, we will be using the following dataset:


```r
library(downloader) 
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/mice_pheno.csv"
filename <- basename(url)
if (!file.exists(filename)) download(url,destfile = filename)
dat <- read.csv(filename)
```

We will remove the lines that contain missing values:


```r
dat <- na.omit( dat )
```

## Population, Samples, and Estimates Exercises #1

Use dplyr to create a vector x with the body weight of all males on the control (chow) diet. What is this population's average?


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
x <- dat %>% filter(Sex == "M", Diet == "chow") %>% select(Bodyweight) %>% unlist
Xbar <- mean(x)
Xbar
```

```
## [1] 30.96381
```

## Population, Samples, and Estimates Exercises #2

Now use the rafalib package and use the popsd function to compute the population standard deviation.


```r
library(rafalib)
popsd(x)
```

```
## [1] 4.420501
```

## Population, Samples, and Estimates Exercises #3

Set the seed at 1. Take a random sample  of size 25 from x. What is the sample average?


```r
set.seed(1)
xbar <- mean(sample(x, 25))
xbar
```

```
## [1] 32.0956
```

## Population, Samples, and Estimates Exercises #4

Use dplyr to create a vector y with the body weight of all males on the high fat hf) diet. What is this population's average?


```r
y <- dat %>% filter(Sex == "M", Diet == "hf") %>% select(Bodyweight) %>% unlist
Ybar <- mean(y)
Ybar
```

```
## [1] 34.84793
```

## Population, Samples, and Estimates Exercises #5

Now use the rafalib package and use the popsd function to compute the population standard deviation.


```r
popsd(y)
```

```
## [1] 5.574609
```

## Population, Samples, and Estimates Exercises #6

Set the seed at 1. Take a random sample  of size 25 from y. What is the sample average?


```r
set.seed(1)
ybar <- mean(sample(y, 25))
ybar
```

```
## [1] 34.768
```

## Population, Samples, and Estimates Exercises #7

What is the difference in absolute value between difference in sample means and the difference in population means?


```r
abs((ybar - xbar) - (Ybar - Xbar)) 
```

```
## [1] 1.211716
```


## Population, Samples, and Estimates Exercises #8

Repeat the above for females. Make sure to set the seed to 1 before each sample call. What is the difference in absolute value between and ?


```r
x <- dat %>% filter(Sex == "F", Diet == "chow") %>% select(Bodyweight) %>% unlist
Xbar <- mean(x)

set.seed(1)
xbar <- mean(sample(x, 25))

y <- dat %>% filter(Sex == "F", Diet == "hf") %>% select(Bodyweight) %>% unlist
Ybar <- mean(y)

set.seed(1)
ybar <- mean(sample(y, 25))

abs((ybar - xbar) - (Ybar - Xbar))
```

```
## [1] 0.7364828
```


## Population, Samples, and Estimates Exercises #9

For the females, our sample estimates were closer to the population difference than with males. What is a possible explanation for this?


```r
dat %>% group_by(Sex) %>% summarize(sd = sd(Bodyweight))
```

```
## # A tibble: 2 x 2
##   Sex      sd
##   <fct> <dbl>
## 1 F      4.44
## 2 M      5.36
```

* **The population variance of the females is smaller than that of the males; thus, the sample variable has less variability.**

* Statistical estimates are more precise for females.

* The sample size was larger for females.

* The sample size was smaller for females.

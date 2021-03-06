---
title: "Central Limit Theorem Exercises"
author: "Sean Angiolillo"
date: "8 March 2018"
output: 
  html_document: 
    keep_md: yes
---



For these exercises, we will be using the following dataset:


```r
library(downloader) 
library(rafalib)
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/mice_pheno.csv"
filename <- basename(url)
if (!file.exists(filename)) download(url,destfile = filename)
dat <- na.omit( read.csv(filename) )
```

## Central Limit Theorem Exercises #1

If a list of numbers has a distribution that is well approximated by the normal distribution, what proportion of these numbers are within one standard deviation away from the list's average?


```r
pnorm(1) - pnorm(-1)
```

```
## [1] 0.6826895
```

## Central Limit Theorem Exercises #2

What proportion of these numbers are within two standard deviations away from the list's average?


```r
pnorm(2) - pnorm(-2)
```

```
## [1] 0.9544997
```

## Central Limit Theorem Exercises #3

What proportion of these numbers are within three standard deviations away from the list's average?


```r
pnorm(3) - pnorm(-3)
```

```
## [1] 0.9973002
```

## Central Limit Theorem Exercises #4

Define y to be the weights of males on the control diet. What proportion of the mice are within one standard deviation away from the average weight (remember to use popsd for the population sd)?


```r
library(dplyr)
y <- dat %>% filter(Sex == "M", Diet == "chow") %>% select(Bodyweight) %>% unlist
#mean(y < mean(y) + popsd(y)) - mean(y < mean(y) - popsd(y))
#mean((y < mean(y) + popsd(y)) & (y > mean(y) - popsd(y))) 
z <- (y - mean(y)) / popsd(y)
mean(abs(z) <= 1)
```

```
## [1] 0.6950673
```

## Central Limit Theorem Exercises #5

What proportion of these numbers are within two standard deviations away from the list's average?


```r
mean(abs(z) <= 2)
```

```
## [1] 0.9461883
```

## Central Limit Theorem Exercises #6

What proportion of these numbers are within three standard deviations away from the list's average?


```r
mean(abs(z) <= 3)
```

```
## [1] 0.9910314
```

## Central Limit Theorem Exercises #7

Note that the numbers for the normal distribution and our weights are relatively close. Also, notice that we are indirectly comparing quantiles of the normal distribution to quantiles of the mouse weight distribution. We can actually compare all quantiles using a qqplot. Which of the following best describes the qq-plot comparing mouse weights to the normal distribution?


```r
# qq-plot comparing mouse weights to the normal distribution
qqnorm(z)
abline(0,1)
```

![](clt_exercises_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

* The points on the qq-plot fall exactly on the identity line.

* The average of the mouse weights is not 0 and thus it can't follow a normal distribution.

* **The mouse weights are well approximated by the normal distribution, although the larger values (right tail) are larger than predicted by the normal. This is consistent with the differences seen between question 3 and 6.**

* These are not random variables and thus they can't follow a normal distribution.

## Central Limit Theorem Exercises #8

Create the above qq-plot for the four populations: male/females on each of the two diets. What is the most likely explanation for the mouse weights being well approximated? What is the best explanation for all these being well approximated by the normal distribution?


```r
# qq-plot for the four populations: male/females on each of the two diets
mypar(2,2)
y <- filter(dat, Sex=="M" & Diet=="chow") %>% select(Bodyweight) %>% unlist
z <- ( y - mean(y) ) / popsd(y)
qqnorm(z);abline(0,1)
y <- filter(dat, Sex=="F" & Diet=="chow") %>% select(Bodyweight) %>% unlist
z <- ( y - mean(y) ) / popsd(y)
qqnorm(z);abline(0,1)
y <- filter(dat, Sex=="M" & Diet=="hf") %>% select(Bodyweight) %>% unlist
z <- ( y - mean(y) ) / popsd(y)
qqnorm(z);abline(0,1)
y <- filter(dat, Sex=="F" & Diet=="hf") %>% select(Bodyweight) %>% unlist
z <- ( y - mean(y) ) / popsd(y)
qqnorm(z);abline(0,1)
```

![](clt_exercises_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

* The CLT tells us that sample averages are approximately normal.

* **This just happens to be how nature behaves in this particular case. Perhaps the result of many biological factors averaging out.**

* Everything measured in nature follows a normal distribution.

* Measurement error is normally distributed.

## Central Limit Theorem Exercises #9

Here we are going to use the function replicate to learn about the distribution of random variables. All the above exercises relate to the normal distribution as an approximation of the distribution of a fixed list of numbers or a population. We have not yet discussed probability in these exercises. If the distribution of a list of numbers is approximately normal, then if we pick a number at random from this distribution, it will follow a normal distribution. However, it is important to remember that stating that some quantity has a distribution does not necessarily imply this quantity is random. Also, keep in mind that this is not related to the central limit theorem. The central limit applies to averages of random variables. Let's explore this concept.

We will now take a sample of size 25 from the population of males on the chow diet. The average of this sample is our random variable. We will use the replicate to observe 10,000 realizations of this random variable. Set the seed at 1, generate these 10,000 averages. Make a histogram and qq-plot of these 10,000 numbers against the normal distribution.

We can see that, as predicted by the CLT, the distribution of the random variable is very well approximated by the normal distribution.


```r
y <- filter(dat, Sex == "M" & Diet == "chow") %>% select(Bodyweight) %>% unlist
avgs <- replicate(10000, mean( sample(y, 25)))
mypar(1,2)
hist(avgs)
qqnorm(avgs)
qqline(avgs)
```

![](clt_exercises_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

What is the average of the distribution of the sample average?


```r
mean(avgs)
```

```
## [1] 30.97026
```

## Central Limit Theorem Exercises #10

What is the standard deviation of the distribution of sample averages?


```r
popsd(avgs)
```

```
## [1] 0.8279079
```


---
title: "Random Variables Exercises"
author: "Sean Angiolillo"
date: "8 March 2018"
output: 
  html_document: 
    keep_md: yes
---



For these exercises, we will be using the following dataset:

```r
library(downloader) 
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/femaleControlsPopulation.csv"
filename <- basename(url)
if (!file.exists(filename)) download(url,destfile = filename)
x <- unlist( read.csv(filename) )
```

Here x represents the weights for the entire population.

## Random Variables Exercises #1

What is the average of these weights?


```r
mean(x)
```

```
## [1] 23.89338
```

## Random Variables Exercises #2

After setting the seed at 1, set.seed(1) take a random sample of size 5. What is the absolute value (use abs) of the difference between the average of the sample and the average of all the values?


```r
set.seed(1)
abs(mean(x) - mean(sample(x, 5)))
```

```
## [1] 0.2706222
```

## Random Variables Exercises #3

After setting the seed at 5, set.seed(5) take a random sample of size 5. What is the absolute value of the difference between the average of the sample and the average of all the values?


```r
set.seed(5)
abs(mean(x) - mean(sample(x, 5)))
```

```
## [1] 1.433378
```

## Random Variables Exercises #4

Why are the answers from 2 and 3 different?

* Because we made a coding mistake.

* Because the average of the x is random.

* **Because the average of the samples is a random variable.**

* All of the above.
unanswered

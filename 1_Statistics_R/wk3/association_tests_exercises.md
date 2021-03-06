---
title: "Association Tests Exercises"
author: "Sean Angiolillo"
date: "3/21/2018"
output: 
  html_document: 
    keep_md: yes
---



In the previous video, Rafa showed how to calculate a Chi-square test from a table. Here we will show how to generate the table from data which is in the form of a dataframe, so that you can then perform an association test to see if two columns have an enrichment (or depletion) of shared occurances.

Download the assoctest.csv file into your R working directory, and then read it into R:


```r
library(downloader)
url <- "https://prod-edxapp.edx-cdn.org/assets/courseware/v1/f3b6df96b94a01d80e35e3cecf3d83f0/asset-v1:HarvardX+PH525.1x+1T2018+type@asset+block/assoctest.csv"
filename <- basename(url)
if (!file.exists(filename)) download(url,destfile = filename)
d <- read.csv("assoctest.csv")
```

This dataframe reflects the allele status (either AA/Aa or aa) and the case/control status for 72 individuals.

## Association Tests Exercises #1

Compute the Chi-square test for the association of genotype with case/control status (using the `table()` function and the `chisq.test()` function). Examine the table to see if it look enriched for association by eye. What is the X-squared statistic?


```r
chisq.test(table(d))$statistic
```

```
## X-squared 
##  3.343653
```

## Association Tests Exercises #2

Compute the Fisher's exact test ( `fisher.test()` ) for the same table. What is the p-value?


```r
fisher.test(table(d))$p.value
```

```
## [1] 0.05193834
```


---
title: "First assessment: Run swirl Exercises"
author: "Sean Angiolillo"
date: "3/7/2018"
output: 
  html_document: 
    keep_md: yes
---



## Run swirl Exercises #1

What version of R are you using (hint: make sure you download the latest version and then type version)? Please note that this question does not count toward your grade, but it is important to make sure that you are using the latest version of R. If the answer is not the MOST updated, please just let us know.


```r
version
```

```
##                _                           
## platform       x86_64-apple-darwin13.4.0   
## arch           x86_64                      
## os             darwin13.4.0                
## system         x86_64, darwin13.4.0        
## status                                     
## major          3                           
## minor          3.2                         
## year           2016                        
## month          10                          
## day            31                          
## svn rev        71607                       
## language       R                           
## version.string R version 3.3.2 (2016-10-31)
## nickname       Sincere Pumpkin Patch
```

## Run swirl Exercises #2

Create a numeric vector containing the numbers 2.23, 3.45, 1.87, 2.11, 7.33, 18.34, 19.23. What is the average of these numbers?


```r
mean(c(2.23, 3.45, 1.87, 2.11, 7.33, 18.34, 19.23))
```

```
## [1] 7.794286
```

## Run swirl Exercises #3

Use a for loop to determine the value of the sum of numbers 1 to 25 squared.


```r
total <- 0
for (i in 1:25) { 
    total <- total + i^2
}
total
```

```
## [1] 5525
```

## Run swirl Exercises #4

The cars dataset is available in base R. You can type cars to see it. Use the class function to determine what type of object is cars.


```r
class(cars)
```

```
## [1] "data.frame"
```

## Run swirl Exercises #5

How many rows does the cars object have?


```r
nrow(cars)
```

```
## [1] 50
```

## Run swirl Exercises #6

What is the name of the second column of cars?


```r
names(cars)[2]
```

```
## [1] "dist"
```

## Run swirl Exercises #7

The simplest way to extract the columns of a matrix or data.frame is using [. For example you can access the second column with cars[,2]. What is the average distance traveled in this dataset?


```r
mean(cars[,2])
```

```
## [1] 42.98
```

## Run swirl Exercises #8

Familiarize yourself with the which function. What row of cars has a a distance of 85?


```r
which(cars$dist == 85)
```

```
## [1] 50
```



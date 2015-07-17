# Reproducible Research: Peer Assessment 1

## Housekeeping

Clear Environment and Console

```r
rm(list=ls())
cat('\014')
```

packageR is a function used to install R Packages.
packageR is invoked, and packages installed, only when needed


```r
packageR <- function(pkg){
     if (!require(pkg,character.only = TRUE))
     {
          install.packages(pkg,dep=TRUE)
          if(!require(pkg,character.only = TRUE)) {
               stop("Package not found")
          } else {
               library(pkg,character.only=TRUE)
          }
     }
}

packageR("datasets")
packageR("ProjectTemplate")
```

```
## Loading required package: ProjectTemplate
```

```r
packageR("ggplot2")
```

```
## Loading required package: ggplot2
```

```r
packageR("rmarkdown")
```

```
## Loading required package: rmarkdown
```

```r
packageR("data.table")
```

```
## Loading required package: data.table
```

```r
packageR("dplyr")
```

```
## Loading required package: dplyr
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:data.table':
## 
##     between, last
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
packageR("lubridate")
```

```
## Loading required package: lubridate
## 
## Attaching package: 'lubridate'
## 
## The following objects are masked from 'package:data.table':
## 
##     hour, mday, month, quarter, wday, week, yday, year
```

pathR is a function to simplify multi-device development.
pathR is used to set 'path_to_data' as appropriate for my machines


```r
pathR <- function(machine,course){
     machine.path <- "/Users/rickwrites/Dropbox/Data-Science/Coursera/"
     if(machine != "iMac"){
          machine.path <- "/Users/Rick/Dropbox/Data-Science/Coursera/"
     }
     paste(machine.path,course,sep="")
}

getwd()
course <- "DS-05-Reproducible"
working.directory <- pathR('iMac',course)
setwd(working.directory) ## Make it so, Number One (set the Working Directory to the applicable path for current machine)
getwd()
```


## Loading and preprocessing the data



## What is mean total number of steps taken per day?



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


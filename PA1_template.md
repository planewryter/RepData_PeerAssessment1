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
course <- "DS-05-Reproducible/RepData_PeerAssessment1"
working.directory <- pathR('iMac',course)
setwd(working.directory) ## Make it so, Number One (set the Working Directory to the applicable path for current machine)
getwd()
```

## Loading and preprocessing the data


```r
csv.name <- "activity.csv"

if (!file.exists(csv.name)){
     unzip("activity.zip")
}

activity.dt <- fread("activity.csv",na.string="NA")

print(str(activity.dt))
```

```
## Classes 'data.table' and 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
##  - attr(*, ".internal.selfref")=<externalptr> 
## NULL
```

```r
print(nrow(activity.dt))
```

```
## [1] 17568
```

```r
head(activity.dt,20)
```

```
##     steps       date interval
##  1:    NA 2012-10-01        0
##  2:    NA 2012-10-01        5
##  3:    NA 2012-10-01       10
##  4:    NA 2012-10-01       15
##  5:    NA 2012-10-01       20
##  6:    NA 2012-10-01       25
##  7:    NA 2012-10-01       30
##  8:    NA 2012-10-01       35
##  9:    NA 2012-10-01       40
## 10:    NA 2012-10-01       45
## 11:    NA 2012-10-01       50
## 12:    NA 2012-10-01       55
## 13:    NA 2012-10-01      100
## 14:    NA 2012-10-01      105
## 15:    NA 2012-10-01      110
## 16:    NA 2012-10-01      115
## 17:    NA 2012-10-01      120
## 18:    NA 2012-10-01      125
## 19:    NA 2012-10-01      130
## 20:    NA 2012-10-01      135
```

## What is mean total number of steps taken per day?
Note from Instructions: "...ignore the missing values in the dataset""


```r
steps.mean.by.day <- activity.dt[,lapply(.SD,mean,na.rm=TRUE),by=date,.SDcols='steps']
print(format(steps.mean.by.day,digits=3))
```

```
##       date         steps   
##  [1,] "2012-10-01" "   NaN"
##  [2,] "2012-10-02" " 0.438"
##  [3,] "2012-10-03" "39.417"
##  [4,] "2012-10-04" "42.069"
##  [5,] "2012-10-05" "46.160"
##  [6,] "2012-10-06" "53.542"
##  [7,] "2012-10-07" "38.247"
##  [8,] "2012-10-08" "   NaN"
##  [9,] "2012-10-09" "44.483"
## [10,] "2012-10-10" "34.375"
## [11,] "2012-10-11" "35.778"
## [12,] "2012-10-12" "60.354"
## [13,] "2012-10-13" "43.146"
## [14,] "2012-10-14" "52.424"
## [15,] "2012-10-15" "35.205"
## [16,] "2012-10-16" "52.375"
## [17,] "2012-10-17" "46.708"
## [18,] "2012-10-18" "34.917"
## [19,] "2012-10-19" "41.073"
## [20,] "2012-10-20" "36.094"
## [21,] "2012-10-21" "30.628"
## [22,] "2012-10-22" "46.736"
## [23,] "2012-10-23" "30.965"
## [24,] "2012-10-24" "29.010"
## [25,] "2012-10-25" " 8.653"
## [26,] "2012-10-26" "23.535"
## [27,] "2012-10-27" "35.135"
## [28,] "2012-10-28" "39.785"
## [29,] "2012-10-29" "17.424"
## [30,] "2012-10-30" "34.094"
## [31,] "2012-10-31" "53.521"
## [32,] "2012-11-01" "   NaN"
## [33,] "2012-11-02" "36.806"
## [34,] "2012-11-03" "36.705"
## [35,] "2012-11-04" "   NaN"
## [36,] "2012-11-05" "36.247"
## [37,] "2012-11-06" "28.938"
## [38,] "2012-11-07" "44.733"
## [39,] "2012-11-08" "11.177"
## [40,] "2012-11-09" "   NaN"
## [41,] "2012-11-10" "   NaN"
## [42,] "2012-11-11" "43.778"
## [43,] "2012-11-12" "37.378"
## [44,] "2012-11-13" "25.472"
## [45,] "2012-11-14" "   NaN"
## [46,] "2012-11-15" " 0.142"
## [47,] "2012-11-16" "18.892"
## [48,] "2012-11-17" "49.788"
## [49,] "2012-11-18" "52.465"
## [50,] "2012-11-19" "30.698"
## [51,] "2012-11-20" "15.528"
## [52,] "2012-11-21" "44.399"
## [53,] "2012-11-22" "70.927"
## [54,] "2012-11-23" "73.590"
## [55,] "2012-11-24" "50.271"
## [56,] "2012-11-25" "41.090"
## [57,] "2012-11-26" "38.757"
## [58,] "2012-11-27" "47.382"
## [59,] "2012-11-28" "35.358"
## [60,] "2012-11-29" "24.469"
## [61,] "2012-11-30" "   NaN"
```



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


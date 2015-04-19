# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

First, read and unzip the file in the following way:


```r
unzip('./activity.zip', overwrite = TRUE)
activityData <- read.csv2('./activity.csv', sep=',')
```

## What is mean total number of steps taken per day?

The analysis assumes that the analyst has the following packages installed on the machine: 

- dplyr 
- ggplot2


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
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
library(ggplot2)
stepsPerDay <- summarise(group_by(activityData, date), steps_per_day=sum(steps, rm.na=TRUE))
meanStepsPerDay <- mean(stepsPerDay$steps_per_day, na.rm=TRUE)
medianStepsPerDay <- median(stepsPerDay$steps_per_day, na.rm=TRUE)
```
The average number of steps per day is: 1.0767189\times 10^{4}. The median number of steps per day is: 10766.

To visualize the distribution of total steps per day, the following command is executed:


```r
 qplot(stepsPerDay$steps_per_day, data=stepsPerDay, geom="histogram", xlim=c(0,22500), xlab='Total Steps Per Day', ylab='Count', binwidth=2000)
```

![](PA1_template_files/figure-html/steps_per_day_historgram-1.png) 


## What is the average daily activity pattern?



## Imputing missing values

Let's find out how many missing values there are: 

```r
missingValues <- activityData[is.na(activityData$steps),]
numberOfMissingValues <- length(missingValues)
```
There are 3

## Are there differences in activity patterns between weekdays and weekends?

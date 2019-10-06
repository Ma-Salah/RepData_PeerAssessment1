---
output: 
  html_document: 
    fig_caption: yes
    keep_md: yes
---
This is Reproducible Research Project 1
==========================================

For step 1: getting and processing data


```r
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 3.6.1
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
mydata <- read.csv("activity.csv", sep = ",")
mydata <- tbl_df(mydata)
```

Step 2: Histogram of the total number of steps taken each day


```r
totalsteps <- tapply(mydata$steps, mydata$date, sum)
hist(totalsteps, main = "Total number of steps taken each day", col = "red")
```

![](PA1_template_files/figure-html/step2-1.png)<!-- -->

```r
dev.copy(png, file = "Step 2.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

Step 3: Mean and median number of steps taken each day
mean

```r
tapply(mydata$steps, mydata$date, mean)
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##         NA  0.4375000 39.4166667 42.0694444 46.1597222 53.5416667 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
## 38.2465278         NA 44.4826389 34.3750000 35.7777778 60.3541667 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
## 43.1458333 52.4236111 35.2048611 52.3750000 46.7083333 34.9166667 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
## 41.0729167 36.0937500 30.6284722 46.7361111 30.9652778 29.0104167 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##  8.6527778 23.5347222 35.1354167 39.7847222 17.4236111 34.0937500 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
## 53.5208333         NA 36.8055556 36.7048611         NA 36.2465278 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
## 28.9375000 44.7326389 11.1770833         NA         NA 43.7777778 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
## 37.3784722 25.4722222         NA  0.1423611 18.8923611 49.7881944 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
## 52.4652778 30.6979167 15.5277778 44.3993056 70.9270833 73.5902778 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
## 50.2708333 41.0902778 38.7569444 47.3819444 35.3576389 24.4687500 
## 2012-11-30 
##         NA
```
medain

```r
tapply(mydata$steps, mydata$date, median)
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##         NA          0          0          0          0          0 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##          0         NA          0          0          0          0 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##          0          0          0          0          0          0 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##          0          0          0          0          0          0 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##          0          0          0          0          0          0 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##          0         NA          0          0         NA          0 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##          0          0          0         NA         NA          0 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##          0          0         NA          0          0          0 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##          0          0          0          0          0          0 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##          0          0          0          0          0          0 
## 2012-11-30 
##         NA
```

Step 4: Time series plot of the average number of steps taken

```r
avsteps <-tapply(mydata$steps, mydata$interval, mean, na.rm = TRUE)
mydata <- transform(mydata, interval = as.factor(interval))
plot(levels(mydata$interval),avsteps, type = "l", main = "Average number of steps",xlab = "5-minute interval", ylab = "Average of steps in all days")
```

![](PA1_template_files/figure-html/step-1.png)<!-- -->

```r
dev.copy(png, file = "Step 4.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

step 5: The 5-minute interval that, on average, contains the maximum number of steps

```r
x <- mydata[max(na.omit(mydata$steps)),"interval"]
as.numeric(as.character(x))
```

```
## [1] 1905
```

step 6: Code to describe and show a strategy for imputing missing data
Number of missing values

```r
s <- mydata$steps
length(s) - length(na.omit(s))
```

```
## [1] 2304
```
Filling in all of the missing values with mean values

```r
mydata <- transform(mydata, date= as.character(date))
nas <- which(is.na(mydata$steps))
df <- na.omit(mydata)
step <- tapply(df$steps, df$date, sum)
mean <- mean(step)
newdata <- mydata
newdata$steps[nas] <- mean
```

Step 7: Histogram of the total number of steps taken each day after missing values are imputed

```r
newsteps <- tapply(newdata$steps, newdata$date, sum)
newsteps <- as.numeric(newsteps)
hist(newsteps, main = "Total number of steps taken each day after missing values are imputed", col = "red")
```

![](PA1_template_files/figure-html/step7-1.png)<!-- -->

mean total number of steps taken per day

```r
as.integer(tapply(newdata$steps, newdata$date, mean))
```

```
##  [1] 10766     0    39    42    46    53    38 10766    44    34    35
## [12]    60    43    52    35    52    46    34    41    36    30    46
## [23]    30    29     8    23    35    39    17    34    53 10766    36
## [34]    36 10766    36    28    44    11 10766 10766    43    37    25
## [45] 10766     0    18    49    52    30    15    44    70    73    50
## [56]    41    38    47    35    24 10766
```

medain total number of steps taken per day

```r
as.integer(tapply(newdata$steps, newdata$date, median))
```

```
##  [1] 10766     0     0     0     0     0     0 10766     0     0     0
## [12]     0     0     0     0     0     0     0     0     0     0     0
## [23]     0     0     0     0     0     0     0     0     0 10766     0
## [34]     0 10766     0     0     0     0 10766 10766     0     0     0
## [45] 10766     0     0     0     0     0     0     0     0     0     0
## [56]     0     0     0     0     0 10766
```

Step 8: Panel plot comparing the average number of steps taken per 5-minute interval across weekdays and weekends

```r
days <- newdata$date
days <- as.character(days)
days <- as.Date(days)
days <- weekdays(days)
Sys.setlocale("LC_ALL", "English")
```

```
## [1] "LC_COLLATE=English_United States.1252;LC_CTYPE=English_United States.1252;LC_MONETARY=English_United States.1252;LC_NUMERIC=C;LC_TIME=English_United States.1252"
```

```r
for(i in 1:length(days)){
     if (days[i]=="Saturday") {days[i] <- "weekend"}
     else {(days[i] <- "weekday")}
}
newdata <- mutate(newdata, days)
newdata <- transform(newdata, days=as.factor(days))
wend <- filter(newdata, days=="weekend")
wday <- filter(newdata, days=="weekday")
wendm <- tapply(wend$steps, wend$interval, mean)
wdaym <- tapply(wday$steps, wday$interval, mean)
```


```r
par(mfrow=c(1,2))
plot(levels(mydata$interval), wendm, ylim = c(1350,1600), type = "l", xlab = "Interval",ylab = "steps", main = "Weekend")
plot(levels(mydata$interval), wdaym, ylim = c(1350,1600), type = "l", xlab = "Interval",ylab = "steps", main = "Weekday")
```

<img src="fig/plot-1.png" style="display: block; margin: auto;" />

---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

## Libraries and global options

```r
library(tidyverse)
library(VIM)

#Set echo to True for all chunks, no messages and no warnings
knitr::opts_chunk$set(echo = T,
                      message = FALSE, 
                      warning = F)
```


## 1) Loading and preprocessing the data

```r
activity<-read_csv("activity.csv")
```



## 2) What is mean total number of steps taken per day?

In the next table the total steps per day are shown


```r
#Object with the sum of steps per day
act_per_day<-
      activity %>% 
      group_by(date)%>%
      summarise(steps_per_day=sum(steps,na.rm=T)) %>% 
      ungroup()

knitr::kable(act_per_day,format = "html", table.attr = "style='width:30%;'")
```

<table style='width:30%;'>
 <thead>
  <tr>
   <th style="text-align:left;"> date </th>
   <th style="text-align:right;"> steps_per_day </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2012-10-01 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-02 </td>
   <td style="text-align:right;"> 126 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-03 </td>
   <td style="text-align:right;"> 11352 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-04 </td>
   <td style="text-align:right;"> 12116 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-05 </td>
   <td style="text-align:right;"> 13294 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-06 </td>
   <td style="text-align:right;"> 15420 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-07 </td>
   <td style="text-align:right;"> 11015 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-08 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-09 </td>
   <td style="text-align:right;"> 12811 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-10 </td>
   <td style="text-align:right;"> 9900 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-11 </td>
   <td style="text-align:right;"> 10304 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-12 </td>
   <td style="text-align:right;"> 17382 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-13 </td>
   <td style="text-align:right;"> 12426 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-14 </td>
   <td style="text-align:right;"> 15098 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-15 </td>
   <td style="text-align:right;"> 10139 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-16 </td>
   <td style="text-align:right;"> 15084 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-17 </td>
   <td style="text-align:right;"> 13452 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-18 </td>
   <td style="text-align:right;"> 10056 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-19 </td>
   <td style="text-align:right;"> 11829 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-20 </td>
   <td style="text-align:right;"> 10395 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-21 </td>
   <td style="text-align:right;"> 8821 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-22 </td>
   <td style="text-align:right;"> 13460 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-23 </td>
   <td style="text-align:right;"> 8918 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-24 </td>
   <td style="text-align:right;"> 8355 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-25 </td>
   <td style="text-align:right;"> 2492 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-26 </td>
   <td style="text-align:right;"> 6778 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-27 </td>
   <td style="text-align:right;"> 10119 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-28 </td>
   <td style="text-align:right;"> 11458 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-29 </td>
   <td style="text-align:right;"> 5018 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-30 </td>
   <td style="text-align:right;"> 9819 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-31 </td>
   <td style="text-align:right;"> 15414 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-01 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-02 </td>
   <td style="text-align:right;"> 10600 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-03 </td>
   <td style="text-align:right;"> 10571 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-04 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-05 </td>
   <td style="text-align:right;"> 10439 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-06 </td>
   <td style="text-align:right;"> 8334 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-07 </td>
   <td style="text-align:right;"> 12883 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-08 </td>
   <td style="text-align:right;"> 3219 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-09 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-10 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-11 </td>
   <td style="text-align:right;"> 12608 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-12 </td>
   <td style="text-align:right;"> 10765 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-13 </td>
   <td style="text-align:right;"> 7336 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-14 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-15 </td>
   <td style="text-align:right;"> 41 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-16 </td>
   <td style="text-align:right;"> 5441 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-17 </td>
   <td style="text-align:right;"> 14339 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-18 </td>
   <td style="text-align:right;"> 15110 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-19 </td>
   <td style="text-align:right;"> 8841 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-20 </td>
   <td style="text-align:right;"> 4472 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-21 </td>
   <td style="text-align:right;"> 12787 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-22 </td>
   <td style="text-align:right;"> 20427 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-23 </td>
   <td style="text-align:right;"> 21194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-24 </td>
   <td style="text-align:right;"> 14478 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-25 </td>
   <td style="text-align:right;"> 11834 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-26 </td>
   <td style="text-align:right;"> 11162 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-27 </td>
   <td style="text-align:right;"> 13646 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-28 </td>
   <td style="text-align:right;"> 10183 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-29 </td>
   <td style="text-align:right;"> 7047 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-30 </td>
   <td style="text-align:right;"> 0 </td>
  </tr>
</tbody>
</table>


```r
#histogram
act_per_day %>% 
      ggplot(aes(steps_per_day))+
      geom_histogram(
            fill="dodgerblue4",binwidth = 2000
                  )
```

![](PA1_template_files/figure-html/mean and median-1.png)<!-- -->

```r
#mean and median
act_per_day %>% 
      summarise(mean=mean(steps_per_day,na.rm=T),
                median=median(steps_per_day,na.rm=T))
```

```
## # A tibble: 1 x 2
##    mean median
##   <dbl>  <dbl>
## 1 9354.  10395
```

The mean is 9354 steps per day, and the median is 10395 steps.

## 3) What is the average daily activity pattern?


```r
#mean per interval across al days
act_per_interval<-
   activity %>% 
   group_by(interval)%>%
   summarise(steps_per_interval=mean(steps,na.rm=T)) %>% 
   ungroup()

#time series plot
act_per_interval %>% 
   ggplot(aes(interval,steps_per_interval))+
   geom_line(color="#00BFC4",
             size=1)
```

![](PA1_template_files/figure-html/daily pattern-1.png)<!-- -->

```r
#interval with the maximum number of steps:
act_per_interval$interval[act_per_interval$steps_per_interval==max(act_per_interval$steps_per_interval)]
```

```
## [1] 835
```
The interval with the maximum number of steps is 835.

## 4) Imputing missing values



```r
#TOTAL NUMBER OF ROWS
sum(is.na(activity$steps))
```

```
## [1] 2304
```
There are 2304 missing values in the variable steps.

Now I imput the missing values using KNN (k=5)

```r
act_imp<-activity %>% 
   mutate(
      #I calculate the day of the week to use it as a variable for the imputation 
      day_of_the_week=weekdays(date)
   ) 

#KNN imputation (k=5)
#new dataset:
act_imp<-
   kNN(act_imp,
       imp_var = F
             )
```
New histogram, mean, and median with imputed data

```r
#Object with the sum of steps per day
act_imp_per_day<-
   act_imp %>% 
   group_by(date)%>%
   summarise(steps_imp_per_day=sum(steps)) %>% 
   ungroup()

#histogram
act_imp_per_day %>% 
      ggplot(aes(steps_imp_per_day))+
      geom_histogram(
            fill="#F8766D",binwidth = 2000
                  )
```

![](PA1_template_files/figure-html/new mean and median-1.png)<!-- -->

```r
#mean and median
act_imp_per_day%>% 
      summarise(mean=mean(steps_imp_per_day),
                median=median(steps_imp_per_day))
```

```
## # A tibble: 1 x 2
##    mean median
##   <dbl>  <dbl>
## 1 9918.  10395
```
The mean has increased in 564 steps, but the median hasn't changed. 

Now I will analyze how the total steps per day have changed.


```r
act_difference<-
   act_per_day %>% 
   left_join(act_imp_per_day) %>% 
   mutate(dif=steps_imp_per_day-steps_per_day)


act_difference %>%
  filter(dif!=0)
```

```
## # A tibble: 8 x 4
##   date       steps_per_day steps_imp_per_day   dif
##   <date>             <dbl>             <dbl> <dbl>
## 1 2012-10-01             0              4448  4448
## 2 2012-10-08             0              4448  4448
## 3 2012-11-01             0              5424  5424
## 4 2012-11-04             0              2751  2751
## 5 2012-11-09             0              6052  6052
## 6 2012-11-10             0              3557  3557
## 7 2012-11-14             0              1673  1673
## 8 2012-11-30             0              6052  6052
```

There are only differences between the original dataset and the imputed one in the days that all the values are missing values. That's the reason why the mean increases.



## 5) Are there differences in activity patterns between weekdays and weekends?


```r
act_imp<-act_imp %>% 
   mutate(
      type_of_day=factor(
         if_else(
            #my system is in Spanish. Sábado=Saturday, Domingo=Sunday
            day_of_the_week %in% c("sábado","domingo"),
            "weekend",
            "weekday"
         ),
         levels=c("weekend","weekday")
          )
      ) 

act_type_of_day<-act_imp %>% 
   group_by(type_of_day,interval) %>%
   summarise(steps_int_week=mean(steps)) %>% 
   ungroup()

act_type_of_day %>% 
   ggplot(aes(interval,steps_int_week,color=type_of_day))+
   geom_line(size=1)+
   facet_wrap(~type_of_day,nrow=2,ncol=1)+
   guides(color=F)+
   xlab("Interval")+
   ylab("Number of steps")+
   theme()
```

![](PA1_template_files/figure-html/weekdays and weekends-1.png)<!-- -->

There are different patterns in activity between weekends and weekdays. At weekdays, between the intervals 540 and 905, the steps are significantly higher than weekends.In the rest of the intervals there are usually more steps at weekends.

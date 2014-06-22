Machine Learning Project 
========================================================

First we load the datasets.


```r
setwd('D:\\Data\\datasets')
trainingdata<-read.csv("pml-training.csv",header=TRUE,na.strings=c("NA",""))
testdata<-read.csv("pml-testing.csv",header=TRUE,na.strings=c("NA",""))
```

Now we look at the training data 

```r
str(trainingdata)
```

```
## 'data.frame':	19622 obs. of  160 variables:
##  $ X                       : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ user_name               : Factor w/ 6 levels "adelmo","carlitos",..: 2 2 2 2 2 2 2 2 2 2 ...
##  $ raw_timestamp_part_1    : int  1323084231 1323084231 1323084231 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 1323084232 ...
##  $ raw_timestamp_part_2    : int  788290 808298 820366 120339 196328 304277 368296 440390 484323 484434 ...
##  $ cvtd_timestamp          : Factor w/ 20 levels "02/12/2011 13:32",..: 9 9 9 9 9 9 9 9 9 9 ...
##  $ new_window              : Factor w/ 2 levels "no","yes": 1 1 1 1 1 1 1 1 1 1 ...
##  $ num_window              : int  11 11 11 12 12 12 12 12 12 12 ...
##  $ roll_belt               : num  1.41 1.41 1.42 1.48 1.48 1.45 1.42 1.42 1.43 1.45 ...
##  $ pitch_belt              : num  8.07 8.07 8.07 8.05 8.07 8.06 8.09 8.13 8.16 8.17 ...
##  $ yaw_belt                : num  -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 -94.4 ...
##  $ total_accel_belt        : int  3 3 3 3 3 3 3 3 3 3 ...
##  $ kurtosis_roll_belt      : Factor w/ 396 levels "-0.016850","-0.021024",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_picth_belt     : Factor w/ 316 levels "-0.021887","-0.060755",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_yaw_belt       : Factor w/ 1 level "#DIV/0!": NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_roll_belt      : Factor w/ 394 levels "-0.003095","-0.010002",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_roll_belt.1    : Factor w/ 337 levels "-0.005928","-0.005960",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_yaw_belt       : Factor w/ 1 level "#DIV/0!": NA NA NA NA NA NA NA NA NA NA ...
##  $ max_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_belt          : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_belt            : Factor w/ 67 levels "-0.1","-0.2",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ min_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_belt          : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_belt            : Factor w/ 67 levels "-0.1","-0.2",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_roll_belt     : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_pitch_belt    : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_yaw_belt      : Factor w/ 3 levels "#DIV/0!","0.00",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ var_total_accel_belt    : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_roll_belt        : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_roll_belt           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_pitch_belt          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_pitch_belt       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_pitch_belt          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_yaw_belt            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_yaw_belt         : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_yaw_belt            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ gyros_belt_x            : num  0 0.02 0 0.02 0.02 0.02 0.02 0.02 0.02 0.03 ...
##  $ gyros_belt_y            : num  0 0 0 0 0.02 0 0 0 0 0 ...
##  $ gyros_belt_z            : num  -0.02 -0.02 -0.02 -0.03 -0.02 -0.02 -0.02 -0.02 -0.02 0 ...
##  $ accel_belt_x            : int  -21 -22 -20 -22 -21 -21 -22 -22 -20 -21 ...
##  $ accel_belt_y            : int  4 4 5 3 2 4 3 4 2 4 ...
##  $ accel_belt_z            : int  22 22 23 21 24 21 21 21 24 22 ...
##  $ magnet_belt_x           : int  -3 -7 -2 -6 -6 0 -4 -2 1 -3 ...
##  $ magnet_belt_y           : int  599 608 600 604 600 603 599 603 602 609 ...
##  $ magnet_belt_z           : int  -313 -311 -305 -310 -302 -312 -311 -313 -312 -308 ...
##  $ roll_arm                : num  -128 -128 -128 -128 -128 -128 -128 -128 -128 -128 ...
##  $ pitch_arm               : num  22.5 22.5 22.5 22.1 22.1 22 21.9 21.8 21.7 21.6 ...
##  $ yaw_arm                 : num  -161 -161 -161 -161 -161 -161 -161 -161 -161 -161 ...
##  $ total_accel_arm         : int  34 34 34 34 34 34 34 34 34 34 ...
##  $ var_accel_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_roll_arm         : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_pitch_arm        : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ avg_yaw_arm             : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ stddev_yaw_arm          : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ var_yaw_arm             : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ gyros_arm_x             : num  0 0.02 0.02 0.02 0 0.02 0 0.02 0.02 0.02 ...
##  $ gyros_arm_y             : num  0 -0.02 -0.02 -0.03 -0.03 -0.03 -0.03 -0.02 -0.03 -0.03 ...
##  $ gyros_arm_z             : num  -0.02 -0.02 -0.02 0.02 0 0 0 0 -0.02 -0.02 ...
##  $ accel_arm_x             : int  -288 -290 -289 -289 -289 -289 -289 -289 -288 -288 ...
##  $ accel_arm_y             : int  109 110 110 111 111 111 111 111 109 110 ...
##  $ accel_arm_z             : int  -123 -125 -126 -123 -123 -122 -125 -124 -122 -124 ...
##  $ magnet_arm_x            : int  -368 -369 -368 -372 -374 -369 -373 -372 -369 -376 ...
##  $ magnet_arm_y            : int  337 337 344 344 337 342 336 338 341 334 ...
##  $ magnet_arm_z            : int  516 513 513 512 506 513 509 510 518 516 ...
##  $ kurtosis_roll_arm       : Factor w/ 329 levels "-0.02438","-0.04190",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_picth_arm      : Factor w/ 327 levels "-0.00484","-0.01311",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_yaw_arm        : Factor w/ 394 levels "-0.01548","-0.01749",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_roll_arm       : Factor w/ 330 levels "-0.00051","-0.00696",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_pitch_arm      : Factor w/ 327 levels "-0.00184","-0.01185",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_yaw_arm        : Factor w/ 394 levels "-0.00311","-0.00562",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ max_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_arm             : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_roll_arm            : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_arm           : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_arm             : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_roll_arm      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_pitch_arm     : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_yaw_arm       : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ roll_dumbbell           : num  13.1 13.1 12.9 13.4 13.4 ...
##  $ pitch_dumbbell          : num  -70.5 -70.6 -70.3 -70.4 -70.4 ...
##  $ yaw_dumbbell            : num  -84.9 -84.7 -85.1 -84.9 -84.9 ...
##  $ kurtosis_roll_dumbbell  : Factor w/ 397 levels "-0.0035","-0.0073",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_picth_dumbbell : Factor w/ 400 levels "-0.0163","-0.0233",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ kurtosis_yaw_dumbbell   : Factor w/ 1 level "#DIV/0!": NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_roll_dumbbell  : Factor w/ 400 levels "-0.0082","-0.0096",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_pitch_dumbbell : Factor w/ 401 levels "-0.0053","-0.0084",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ skewness_yaw_dumbbell   : Factor w/ 1 level "#DIV/0!": NA NA NA NA NA NA NA NA NA NA ...
##  $ max_roll_dumbbell       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_picth_dumbbell      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ max_yaw_dumbbell        : Factor w/ 72 levels "-0.1","-0.2",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ min_roll_dumbbell       : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_pitch_dumbbell      : num  NA NA NA NA NA NA NA NA NA NA ...
##  $ min_yaw_dumbbell        : Factor w/ 72 levels "-0.1","-0.2",..: NA NA NA NA NA NA NA NA NA NA ...
##  $ amplitude_roll_dumbbell : num  NA NA NA NA NA NA NA NA NA NA ...
##   [list output truncated]
```

```r
table(trainingdata$classe)
```

```
## 
##    A    B    C    D    E 
## 5580 3797 3422 3216 3607
```

Removing variables with missing values (NAs)

```r
isNASum<-function(x){
  return (sum(is.na(x)))
}


bad_train<-apply(trainingdata,2,isNASum)==19216
train2<-trainingdata[,!bad_train]

bad_test<-apply(testdata,2,isNASum)==20
test2<-testdata[,!bad_test]
```
Remove unuseful variables, keep only numeric ones.

```r
removeVars<-grep("X|user_name|timestamp|new_window|num_window",names(train2))
train3<-(train2[,-c(removeVars,length(train2))])
test3<-(test2[,-c(removeVars,length(test2))])
```

check for near-zero covariates as well as covariates that are highly correlated. Remove them.

```r
library(caret)
```

```
## Warning: package 'caret' was built under R version 3.0.3
```

```
## Loading required package: ggplot2
```

```
## Warning: package 'ggplot2' was built under R version 3.0.3
```

```r
nzv<-nearZeroVar(train3,saveMetrics=TRUE)
nzv
```

```
##                      freqRatio percentUnique zeroVar   nzv
## roll_belt                1.102        6.7781   FALSE FALSE
## pitch_belt               1.036        9.3772   FALSE FALSE
## yaw_belt                 1.058        9.9735   FALSE FALSE
## total_accel_belt         1.063        0.1478   FALSE FALSE
## gyros_belt_x             1.059        0.7135   FALSE FALSE
## gyros_belt_y             1.144        0.3516   FALSE FALSE
## gyros_belt_z             1.066        0.8613   FALSE FALSE
## accel_belt_x             1.055        0.8358   FALSE FALSE
## accel_belt_y             1.114        0.7288   FALSE FALSE
## accel_belt_z             1.079        1.5238   FALSE FALSE
## magnet_belt_x            1.090        1.6665   FALSE FALSE
## magnet_belt_y            1.100        1.5187   FALSE FALSE
## magnet_belt_z            1.006        2.3290   FALSE FALSE
## roll_arm                52.338       13.5256   FALSE FALSE
## pitch_arm               87.256       15.7323   FALSE FALSE
## yaw_arm                 33.029       14.6570   FALSE FALSE
## total_accel_arm          1.025        0.3364   FALSE FALSE
## gyros_arm_x              1.016        3.2769   FALSE FALSE
## gyros_arm_y              1.454        1.9162   FALSE FALSE
## gyros_arm_z              1.111        1.2639   FALSE FALSE
## accel_arm_x              1.017        3.9598   FALSE FALSE
## accel_arm_y              1.140        2.7367   FALSE FALSE
## accel_arm_z              1.128        4.0363   FALSE FALSE
## magnet_arm_x             1.000        6.8240   FALSE FALSE
## magnet_arm_y             1.057        4.4440   FALSE FALSE
## magnet_arm_z             1.036        6.4468   FALSE FALSE
## roll_dumbbell            1.022       84.2065   FALSE FALSE
## pitch_dumbbell           2.277       81.7450   FALSE FALSE
## yaw_dumbbell             1.132       83.4828   FALSE FALSE
## total_accel_dumbbell     1.073        0.2191   FALSE FALSE
## gyros_dumbbell_x         1.003        1.2282   FALSE FALSE
## gyros_dumbbell_y         1.265        1.4168   FALSE FALSE
## gyros_dumbbell_z         1.060        1.0498   FALSE FALSE
## accel_dumbbell_x         1.018        2.1659   FALSE FALSE
## accel_dumbbell_y         1.053        2.3749   FALSE FALSE
## accel_dumbbell_z         1.133        2.0895   FALSE FALSE
## magnet_dumbbell_x        1.098        5.7486   FALSE FALSE
## magnet_dumbbell_y        1.198        4.3013   FALSE FALSE
## magnet_dumbbell_z        1.021        3.4451   FALSE FALSE
## roll_forearm            11.589       11.0896   FALSE FALSE
## pitch_forearm           65.983       14.8558   FALSE FALSE
## yaw_forearm             15.323       10.1468   FALSE FALSE
## total_accel_forearm      1.129        0.3567   FALSE FALSE
## gyros_forearm_x          1.059        1.5187   FALSE FALSE
## gyros_forearm_y          1.037        3.7764   FALSE FALSE
## gyros_forearm_z          1.123        1.5646   FALSE FALSE
## accel_forearm_x          1.126        4.0465   FALSE FALSE
## accel_forearm_y          1.059        5.1116   FALSE FALSE
## accel_forearm_z          1.006        2.9559   FALSE FALSE
## magnet_forearm_x         1.012        7.7668   FALSE FALSE
## magnet_forearm_y         1.247        9.5403   FALSE FALSE
## magnet_forearm_z         1.000        8.5771   FALSE FALSE
```

From above, it looks like there aren't any near-zero covariates. 

We'll look at correlations among covariates.



```r
corrs<-cor(train3)
library(corrplot)
```

```
## Warning: package 'corrplot' was built under R version 3.0.3
```

```r
corrplot(corrs,method="square",tl.cex=0.5)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6.png) 

```r
highCorr<-findCorrelation(corrs,cutoff=0.75)
train4<-cbind(classe=train2$classe,train3[,-highCorr])
test4<-test3[,-highCorr]
```

Split the training data into training/testing for model evaluation

```r
set.seed(1234)
inTrain <-createDataPartition(train4$classe,p=0.75,list=FALSE)
trainPart<-train4[inTrain,]
testPart<-train4[-inTrain,]
```

Random Forest algorithm to predict

```r
library(randomForest)
```

```
## Warning: package 'randomForest' was built under R version 3.0.3
```

```
## randomForest 4.6-7
## Type rfNews() to see new features/changes/bug fixes.
```

```r
rfModel<-randomForest(classe~.,data=trainPart,importance=TRUE,ntree=500)
print(rfModel)
```

```
## 
## Call:
##  randomForest(formula = classe ~ ., data = trainPart, importance = TRUE,      ntree = 500) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 5
## 
##         OOB estimate of  error rate: 0.63%
## Confusion matrix:
##      A    B    C    D    E class.error
## A 4181    3    0    0    1   0.0009558
## B   12 2828    5    1    2   0.0070225
## C    0   13 2535   19    0   0.0124659
## D    0    0   24 2383    5   0.0120232
## E    0    0    2    6 2698   0.0029564
```
in-sample 

```r
out.test<-predict(rfModel,testPart)
table(testPart$classe, out.test)
```

```
##    out.test
##        A    B    C    D    E
##   A 1395    0    0    0    0
##   B    4  945    0    0    0
##   C    0   11  841    3    0
##   D    0    0    7  797    0
##   E    0    0    1    0  900
```
out-sample 

```r
out.test<-predict(rfModel,test4)
answers<- as.vector(out.test[1:20])
#answers = rep("A", 20)
pml_write_files = function(x){
  n = length(x)
  for(i in 1:n){
    filename = paste0("problem_id_",i,".txt")
    write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
  }
}
pml_write_files(answers)
```

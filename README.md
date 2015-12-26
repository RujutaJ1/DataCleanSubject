# DataCleanSubject
This repository is for Project Submission for Data Clean Project for Coursera Course of Data Cleaning for John Hopkins Institute. 
---
title: "DataCleanProject_Rujuta"
author: "Rujuta Joshi"
date: "Friday, December 18, 2015"
output: html_document
--

# Objective of the project : 
The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. 
The Assignment is as follows. 
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

# Steps taken to understand the object : 
When we see how the data is processed, it gives an idea about how to go about joining the various files and selecting the variables. 
SO the collected data was processed in the following manner. 
1. Test and Train Data was seperated 
2. The Acccelerometer and Gyroscope signals were processed. 
3. In the processing of these signals, 
  1. Remove noise
  2. Sample to take 128 readings 
  3. Seperate Gravity and Body acceleration
  4. for each of the samples , get 561 measurements. 
  
To complete the assignment, we need to take the following steps. 
1. its clear, that the Inertial signals, were the intermediate steps, and hence we are not using these files for the further processing, instead, we would be using X_train data.( and X_test data)
2. Take the X Train data, merge it with Features labels, so that the 561 measurements get the name. 
3. merge with subject train data ( subject names) and Activity names 
4. Select the mean and std variables. 
5. do the same steps on the test data. 
6. merge the test and train data together. 
7. Post this, prepare the tidy data. 


#The detailed activities in the project. 

## Step 1 : First Download the Data, and Unzip it. 
```{r}
# first download the data- since its a heavy download, i am putting this as comment, so as to not download everytime. 
# fileurl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
# getwd()
setwd("F:/Rujuta/Coursera/DataCleanSubject")
#download.file(fileurl, destfile="./Data.zip")
#unzip("./Data.zip")
library(dplyr); library(data.table)

```
## Step 2 

```{r}
# setwd("./UCI HAR Dataset")
list.files()
features <- read.table("./features.txt")
setwd("./train")
X_traindata <- read.table("./X_train.txt")
XTrainDataSet <- data.table(X_traindata)
y_traindata <- read.table("./y_train.txt")
YTrainData <- data.table(y_traindata)
subject_traindata <- read.table("./subject_train.txt")
SubjectTrainData <- data.table(subject_traindata)
FeatureData <- data.table(features)
names <- as.character(features$V2)
setnames(TrainData, colnames(TrainData), names)
```
## Step 3
#merge subjectID and Activity name with the test data.
```{r}
dim(YTrainData)
setnames(YTrainData, "Activity")
dim(SubjectTrainData)
setnames(SubjectTrainData, "SubjectID")
TrainData1 <- cbind(SubjectTrainData,YTrainData, TrainData)
dim(TrainData1)
```
## Step 4 
## Do the same activity with test data. 
```{r}
setwd("./test")
list.files()
X_testdata <- read.table("./X_test.txt")
dim(X_testdata)
TestData <- data.table(X_testdata)
setnames(TestData, colnames(TestData), names)
y_testdata <- read.table("./y_test.txt")
YTestData <- data.table(y_testdata)
dim(YTestData)
setnames(YTestData, "Activity")
SUbjectTestData <- fread("./subject_test.txt")
dim(SUbjectTestData)
setnames(SUbjectTestData, "SubjectID")
TestData1 <- cbind(SUbjectTestData,YTestData,TestData)
dim(TestData1)
```
## Step5 
## combine Test and Train Data. 
```{r}
MainData <- rbind(TestData1, TrainData1)
dim(MainData)
# So this is the final Data. 
```
## Step6
## select only the mean and std variables from the data. 
```{r}
MainDataslice1 <- select(MainData, contains("mean"))
MainDataslice2 <- select(MainData, contains("std"))
MainDataSlice3 <- select(MainData, SubjectID,Activity)
MainDataTogether <- cbind(MainDataSlice3, MainDataslice1, MainDataslice2)
dim(MainDataTogether)
# now to give the activity Lables
ActivityLabels <- c("WALKING","WALKING_UPSTAIRS","WALKING DOWNSTAIRS","SITTING","STANDING","LAYING")
MainDataTogether$Activity <- ordered( MainDataTogether$Activity,levels=c(1,2,3,4,5,6),labels=ActivityLabels)
```

# Preparing the tidy data set
# now to give the activity Lables
```{r}
ActivityLabels <- c("WALKING","WALKING_UPSTAIRS","WALKING DOWNSTAIRS","SITTING","STANDING","LAYING")
MainDataTogether$Activity <- ordered( MainDataTogether$Activity,levels=c(1,2,3,4,5,6),labels=ActivityLabels)
```

# Preparing the tidy data set

```{r}
dim(MainDataTogether)
p <- MainDataTogether[,lapply(.SD, mean), by=SubjectID]
dim(p)
q <- MainDataTogether[, lapply(.SD, mean), by=Activity]
AverageBySubject <- select(p, -Activity)
AverageByActivity <- select(q, -SubjectID)
View(AverageBySubject)
View(AverageByActivity)
write.table(AverageByActivity, file="./DataCleanProjectSubmission_Rujuta.txt", append=FALSE, row.names=FALSE)
write.table(AverageBySubject, file="./DataCleanProjectSubmission_Rujuta.txt", append=TRUE, row.names=FALSE)
  # so this is the file that gets uploaded on the github.

THE END






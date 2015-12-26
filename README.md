# DataCleanSubject
This repository is for Project Submission for Data Clean Project for Coursera Course of Data Cleaning for John Hopkins Institute. 
---
title: "DataCleanProject_Rujuta"
author: "Rujuta Joshi"
date: "Friday, December 18, 2015"
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
 Step 1 : First Download the Data, and Unzip it. 
Step 2 : Read the data files, from X Data file, Y Data  and Subject IDs.
Step 3 :merge subjectID and Activity name with the test data.
Step 4 :  Do the same activity with test data. 
Step5 : combine Test and Train Data. 
Step6 :select only the mean and std variables from the data. 
Step 7:  Preparing the tidy data set



Codebook for the output file. 
The file is 180 records having 88 variables.  
The Variables are  SUbject ID, Activity, and All the variables that include either Std or mean in the definition. 
The records are for each subject, by each activity the means of each of the parameter.
The Variable names. 
1	SubjectID
2	Activity
3	tBodyAcc-mean()-X
4	tBodyAcc-mean()-Y
5	tBodyAcc-mean()-Z
6	tGravityAcc-mean()-X
7	tGravityAcc-mean()-Y
8	tGravityAcc-mean()-Z
9	tBodyAccJerk-mean()-X
10	tBodyAccJerk-mean()-Y
11	tBodyAccJerk-mean()-Z
12	tBodyGyro-mean()-X
13	tBodyGyro-mean()-Y
14	tBodyGyro-mean()-Z
15	tBodyGyroJerk-mean()-X
16	tBodyGyroJerk-mean()-Y
17	tBodyGyroJerk-mean()-Z
18	tBodyAccMag-mean()
19	tGravityAccMag-mean()
20	tBodyAccJerkMag-mean()
21	tBodyGyroMag-mean()
22	tBodyGyroJerkMag-mean()
23	fBodyAcc-mean()-X
24	fBodyAcc-mean()-Y
25	fBodyAcc-mean()-Z
26	fBodyAcc-meanFreq()-X
27	fBodyAcc-meanFreq()-Y
28	fBodyAcc-meanFreq()-Z
29	fBodyAccJerk-mean()-X
30	fBodyAccJerk-mean()-Y
31	fBodyAccJerk-mean()-Z
32	fBodyAccJerk-meanFreq()-X
33	fBodyAccJerk-meanFreq()-Y
34	fBodyAccJerk-meanFreq()-Z
35	fBodyGyro-mean()-X
36	fBodyGyro-mean()-Y
37	fBodyGyro-mean()-Z
38	fBodyGyro-meanFreq()-X
39	fBodyGyro-meanFreq()-Y
40	fBodyGyro-meanFreq()-Z
41	fBodyAccMag-mean()
42	fBodyAccMag-meanFreq()
43	fBodyBodyAccJerkMag-mean()
44	fBodyBodyAccJerkMag-meanFreq()
45	fBodyBodyGyroMag-mean()
46	fBodyBodyGyroMag-meanFreq()
47	fBodyBodyGyroJerkMag-mean()
48	fBodyBodyGyroJerkMag-meanFreq()
49	angle(tBodyAccMean,gravity)
50	angle(tBodyAccJerkMean),gravityMean)
51	angle(tBodyGyroMean,gravityMean)
52	angle(tBodyGyroJerkMean,gravityMean)
53	angle(X,gravityMean)
54	angle(Y,gravityMean)
55	angle(Z,gravityMean)
56	tBodyAcc-std()-X
57	tBodyAcc-std()-Y
58	tBodyAcc-std()-Z
59	tGravityAcc-std()-X
60	tGravityAcc-std()-Y
61	tGravityAcc-std()-Z
62	tBodyAccJerk-std()-X
63	tBodyAccJerk-std()-Y
64	tBodyAccJerk-std()-Z
65	tBodyGyro-std()-X
66	tBodyGyro-std()-Y
67	tBodyGyro-std()-Z
68	tBodyGyroJerk-std()-X
69	tBodyGyroJerk-std()-Y
70	tBodyGyroJerk-std()-Z
71	tBodyAccMag-std()
72	tGravityAccMag-std()
73	tBodyAccJerkMag-std()
74	tBodyGyroMag-std()
75	tBodyGyroJerkMag-std()
76	fBodyAcc-std()-X
77	fBodyAcc-std()-Y
78	fBodyAcc-std()-Z
79	fBodyAccJerk-std()-X
80	fBodyAccJerk-std()-Y
81	fBodyAccJerk-std()-Z
82	fBodyGyro-std()-X
83	fBodyGyro-std()-Y
84	fBodyGyro-std()-Z
85	fBodyAccMag-std()
86	fBodyBodyAccJerkMag-std()
87	fBodyBodyGyroMag-std()
88	fBodyBodyGyroJerkMag-std()




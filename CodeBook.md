## Getting and Cleaning Data Project

valyc

## Source Data
A full description of the data used in this project can be found at [The UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

[The source data for this project can be found here.](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)

## Data Set Information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

## Attribute Information
For each record in the dataset it is provided: 
- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

The sourse files used in this project:
- subject_train.txt, Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30
- subject_test.txt, Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30
- X_train.txt, Training set
- X_test.txt, Test set
- y_train.txt, Training labels
- y_test.txt, Test labels
- features.txt, List of all features
- activity_labels.txt, Links the class labels with their activity name

## Step 0. Manualy read data from txt files stored in Working Directory

## Step 1. Merges the training and the test sets to create one data set using rbind and cbind
Combine X test and train data
Combine y test and train data
Combine sunject test and train data
Rename column in features
Insert columns name in X data
Insert column name in y data
Insert columns name in subject data
Create FULL set of data

## Step 2. Extract only the measurements on the mean and standard deviation for each measurement. 
Extract values using grep function for "id", "mean" and "std"

## Step 3. Use descriptive activity names to name the activities in the data set
Transform activities column from integer to character class 
Replace number values by descriptive names

## Step 4. Appropriately label the data set with descriptive variable names
Use gsub function for replacement descriptive variable names

## Step 5. Create a second, independent tidy data set with the average of each variable for each activity and each subject.
Had used aggregate and arrange (dplyr package) functions to create a data set with the average of each variable for each activity and each subject, arranged by activity and subject.
The tidy second data set was saved as txt file.
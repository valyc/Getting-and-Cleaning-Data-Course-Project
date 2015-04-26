## Source Data
A full description of the data used in this project can be found at [The UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

[The source data for this project can be found here.](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)

## Data Set Information
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.

## The sourse files used in this project:
- subject_train.txt, Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30
- subject_test.txt, Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30
- X_train.txt, Training set
- X_test.txt, Test set
- y_train.txt, Training labels
- y_test.txt, Test labels
- features.txt, List of all features
- activity_labels.txt, Links the class labels with their activity name

## Manualy read data from txt files stored in Working Directory
train_subject <- read.table("./UCI HAR Dataset/train/subject_train.txt")
test_subject <- read.table("./UCI HAR Dataset/test/subject_test.txt")
train_x <- read.table("./UCI HAR Dataset/train/X_train.txt")
test_x <- read.table("./UCI HAR Dataset/test/X_test.txt")
train_y <- read.table("./UCI HAR Dataset/train/y_train.txt")
test_y <- read.table("./UCI HAR Dataset/test/y_test.txt")
features <- read.table("./UCI HAR Dataset/features.txt")
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt")

## Task 1. Merges the training and the test sets to create one data set.
# Combine X test and train data
X_full <- rbind(test_x, train_x)
# Combine y test and train data
y_full <- rbind(test_y, train_y)
# Combine sunject test and train data
subject_full <- rbind(test_subject, train_subject)
# Rename column in features
colnames(features) <- c("nr", "name")
# Insert columns name in X data
colnames(X_full) <- features$name
# Insert column name in y data
colnames(y_full) <- "activity_id"
# Insert columns name in subject data
colnames(subject_full) <- "subject_id"
# Create FULL set of data
full_set <- cbind(subject_full, y_full, X_full)

## Task 2. Extract only the measurements on the mean and standard deviation for each measurement.
mean_std_data <- full_set[, grep("id|mean|std", colnames(full_set))]

## Task 3. Uses descriptive activity names to name the activities in the data set
mean_std_data$activity_id <- as.character(mean_std_data$activity_id)
mean_std_data$activity_id[mean_std_data$activity_id == 1] <- "WALKING"
mean_std_data$activity_id[mean_std_data$activity_id == 2] <- "WALKING_UPSTAIRS"
mean_std_data$activity_id[mean_std_data$activity_id == 3] <- "WALKING_DOWNSTAIRS"
mean_std_data$activity_id[mean_std_data$activity_id == 4] <- "SITTING"
mean_std_data$activity_id[mean_std_data$activity_id == 5] <- "STANDING"
mean_std_data$activity_id[mean_std_data$activity_id == 6] <- "LAYING"

## Task 4. Appropriately labels the data set with descriptive variable names. 
names(mean_std_data) <- gsub("Acc", "Accelerator", names(mean_std_data))
names(mean_std_data) <- gsub("Mag", "Magnitude", names(mean_std_data))
names(mean_std_data) <- gsub("Gyro", "Gyroscope", names(mean_std_data))
names(mean_std_data) <- gsub("^t", "time", names(mean_std_data))
names(mean_std_data) <- gsub("^f", "frequency", names(mean_std_data))

## Task 5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
library(dplyr)
tidy_data <- aggregate( . ~ subject_id + activity_id, mean_std_data, mean)
tidy_data <- arrange(tidy_data, subject_id, activity_id)
write.table(tidy_data, file = "Tidy_data.txt", row.names = FALSE)
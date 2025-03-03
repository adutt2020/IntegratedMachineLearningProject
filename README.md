# IntegratedMachineLearningProject
## Sprint 10 - Integrated Project 2 - Machine Learning. 

**Project Summary:** Developed and tuned various regression models to approximate gold recovery, incorporating cross-validation for optimal hyperparameter selection.

**Technical Skills:** Regression analysis, cross-validation, hyperparameter tuning (e.g., GridSearchCV), and model optimization.

## Project Description 

I will be working with data stored in three files from Zyfra, a gold mining company. Data is indexed with the date and time of acquisition (date feature). Parameters that are next to each other in terms of time are often similar.

Some parameters are not available because they were measured and/or calculated much later. That's why, some of the features that are present in the training set may be absent from the test set. The test set also doesn't contain targets.

The source dataset contains the training and test sets with all the features.

I have the raw data that was only downloaded from the warehouse. Before building the model, check the correctness of the data. For that, I will be using the instructions given below:
1. Prepare the data

1.1. Open the files and look into the data.

Path to files:

- /datasets/gold_recovery_train.csv
- /datasets/gold_recovery_test.csv
- /datasets/gold_recovery_full.csv

1.2. Check that recovery is calculated correctly. Using the training set, calculate recovery for the rougher.output.recovery feature. Find the MAE between your calculations and the feature values. Provide findings.

1.3. Analyze the features not available in the test set. What are these parameters? What is their type?

1.4. Perform data preprocessing.

2. Analyze the data

2.1. Take note of how the concentrations of metals (Au, Ag, Pb) change depending on the purification stage.

2.2. Compare the feed particle size distributions in the training set and in the test set. If the distributions vary significantly, the model evaluation will be incorrect.

2.3. Consider the total concentrations of all substances at different stages: raw feed, rougher concentrate, and final concentrate. Do you notice any abnormal values in the total distribution? If you do, is it worth removing such values from both samples? Describe the findings and eliminate anomalies. 

3. Build the model

3.1. Write a function to calculate the final sMAPE value.

3.2. Train different models. Evaluate them using cross-validation. Pick the best model and test it using the test sample. Provide findings.

## Conclusion

**DATA REVIEW**

- I was originally provided three datasets, full data, train data and test data. The train data and test data are from the full data. There is a 75/25 split among the training and testing data. In the training data, there are 87 columns and 16,860 rows. In the test data, there are 53 columns and 5,856 rows. And in the full data, there are 87 columns and 22,716 rows. I was able to find the ratio by the rows of data.
- After further review, I found that there were missing data that I needed to check to see if I could simply drop it or if the values needed to be filled in. 
- There was also incorrect data type for the purpose of this project that needed a conversion.
- Last but not least, I identified the targets as 'rougher.output.recovery' and 'final.output.recovery'

**DATA PREPROCESSING**

- The data type of date has been converted to datetime, and then converted to integers when it came time to test models.
- The missing columns were over 5%, so I filled it in with the column median. 

**EDA**

- CONCENTRATIONS: There is an increase in concentration of gold from the initial purification stage to the final concentrate. It is the highest compared to Silver and Lead. For Silver, there is no increase. It actually decreases throughout all the stages and the final concentrate contains a significantly low amount of concentrate. And for Lead, there is a slight increase, but not a significant one compared to Gold. But it did perform better than Silver.
- OUTLIERS: Based on the histogram for the concentrations, the summed values had a considerable number of outliers as "0". The data in the histogram also showed a right-skewed distribution which can significantly impact the analysis and model-building process. Therefore, I removed the zeros. 
- TRAINING AND TESTING MODELS: Based on the sMAPE values, the lowest value is shown in the Random Forest model. When tested on the test set, the Random Forest model obtained an sMAPE of 11.15.

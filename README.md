# aiml-bank
Assignment #3
Compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines (SVM).

Understanding the Data:
The dataset comes from the UCI Machine Learning repository [link](https://archive.ics.uci.edu/ml/datasets/bank+marketing). 
The data is collected from 17 marketing campaigns over 2.5 years period, contacting more than 79,000 customers.
It resulted in 8% success rate, implying that the dataset is imbalanced.

Understanding Features:
There are 21 columns but we need to create a model only based on the 7 columns for which the back already has the data (prior to marketing campaigns). 

Understanding the Task/Business Objective:
Create multiple models (K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines) based only on the 7 columns for which the bank already has the data (prior to marketing campaigns): [age, job , marital , housing , loan , education, default]. The target variable is ‘y’, which has binary data [yes, no]. Compare the performance of each model.

Engineering Features: Six of the columns for the model have categorical values and have “unknown” value counts as follows:
* job - 330 Unknown values, Action: Delete the rows with Unknown values
* marital - 80 Unknown values, Action: Delete the rows with Unknown values
* housing - 990 Unknown values, Action: Delete the rows with Unknown values
* loan - 990 Unknown values, Action: Delete the rows with Unknown values
* education - 1731 Unknown values, Action: 
* default - 8597 Unknown values, Action: Replace the rows with “unknown” values with “no” since 99.99% of data has value “no”

Changing Categorical Data to Numeric:
* Change y (target): Binary data, change to numeric ([0,1]
* Change housing, loan, default to numeric data
* Use scalers for categorical data (job, marital, education)
Removed the “duration” column from the model features as per instructions in the assignment, since it is not known before a call is performed.

Visualizing Data:
Multiple scatter plots using Seaborn library show the impact of categorical data (job, marital, education) as minimal for most of the rows, except in case when job=retired or student or education=illiterate. Likewise scatter plots of categorical data (age, housing)  also show the impact as minimal for most of the rows.

Train/Test Split:
Splited the data in training and test sets in 0.65 to 0.35 ratio. Created three different X data frames - with 7 features, with only 3 numeric features and with all features. Created a selector to include “object” data types and a transformer to apply OneHot Encode to categorical data and StandardScaler to numeric data.

Baseline Model:
Set baseline accuracy to the most frequently occurring class (y=0 or No), which is 0.8887

Creating and Comparing Models:
Created models using four classifiers:
1. Logistic Regression
2. Decision Trees
3. KNN
4. SVM

The comparison of the Fit-time, Accuracy, Precision and Recall is as follows:
res_dict = {'Model': ['Logistic Regression', 'KNN', 'Decision Tree', 'SVC'],
            'Train Time': [1.5, 180, 2, 300],
            'Accuracy': [0.8879, 0.8877, 0.8710, 0.8879],
            'Precision': [0, 0.2500, 0.2565, 0],
            'Recall': [0, 0.0453, 0.0793, 0]}

Based on the observations above, none of the models performed better than baseline on Accuracy and only KNN and Decision Trees provided some reasonable score for Precision and Recall. So none of the classifier is found to be well suited for the given dataset, based on this initial iteration.

I tried to improve the KNN and Decision Tree classifier models by trying wider range of hyper parameters. The Revised KNN classifier (n_neighbors = 73) provided slightly better scores this time: Accuracy:  0.8999, Precision:  0.6709, Recall:  0.2105. 

Recommendations:
While the Revised KNN classifier is relatively the best but still is only 1% more accurate than baseline and with Recall of 0.2105. A better model in this case should be the one with high er value of Recall to make sure the campaigns do not miss the potential customers.

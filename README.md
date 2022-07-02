# Data Science Project :: Bank-Marketing-Campaign

### Requirements

RStudio ver.1.3.1073

Packages:
dplyr 1.0.2
ggplot2 3.3.5
tidyverse 1.3.0
gplots 3.1.1
car 3.1-11
caret 6.0-86
grid 4.0.2
gridExtra 2.3
rpart 4.1-15
rpart.plot 3.1.0
ggmap 3.0.0
lattice 0.20-41
ROSE 0.0-4

### Data

Data is collected from [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing#)

The data is related with direct marketing campaigns of a Portuguese banking institution. The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed.

The classification goal is to predict if the client will subscribe (yes/no) a term deposit (variable y).

There are four datasests available from the data base, bank-additional-full.csv has 41188 observations and 20 inputs from 2008 - 2010, bank-additional.csv has 10% of the examples (4119) and 20 inputs, bank-full.csv all examples and 17 inputs, which is an older vesion of the data that has less inputs, and bank.csv has 10% of the examples and 17 inputs.

The dataset used for modeling and prediction is the bank-additional.csv, as it contains the newest inputs for measuring. All the categorical variables have been encoded as numbers for classification, and several variables are dropped due to insignificance. There is no missing value or duplicate detected in this dataset, so there is no need for imputation. Outliers are removed using interquartile approach by removing the values below the first quartile and above third quartile.

The distribution of the target variable y shows the data is imbalanced:

<img width="697" alt="Screen Shot 2022-07-02 at 12 40 44 PM" src="https://user-images.githubusercontent.com/103064444/177009043-0709f80c-aa71-49f6-aee4-b676ddac5931.png">

The data is first partitioned into training and validation sets. Then used Over-sampling method to balance the data

<img width="824" alt="Screen Shot 2022-07-02 at 3 01 03 PM" src="https://user-images.githubusercontent.com/103064444/177013201-290a4581-8cfc-4598-a31c-90095bcf3450.png">

### Exploratory Data Analysis

Numeric predictor variables:

<img width="694" alt="Screen Shot 2022-06-17 at 6 38 28 PM" src="https://user-images.githubusercontent.com/103064444/174410094-6992f1ec-89f9-413c-906d-4a825234976b.png">

Note: variable pdays originally has 999 meaning client was not previously contacted, and it has been changed to -1. 999 might be considered as outliers comparing with the other numbers, thus the changed has been made.

The distribution of age in the dataset shows that the age of clients mainly distributed between age 25 and age 50, and there are few outliers after age 60 that skewed the distribution to the right. The distribution of campaign shows that the distribution is skewed to the right with outliers above 10. The distribution of pdays shows that most of the clients were not previously contacted, and only a few of the clients were previously contacted, and the number of days passed since they were contacted skewed the distribution to the right. The distribution of the number of contacts performed before the campaign skewed to the right. The distribution of the employment variation rate is scattered from negative values to one and above. Some of the distributions for numeric variables are skewed to the right but they will not be logged to follow the linearity assuptions because the originality of the data needs to be preserved to predict authentic y. However the accuracy of the prediction might be influenced.

Categorical predictor variables:

<img width="691" alt="Screen Shot 2022-06-17 at 6 53 19 PM" src="https://user-images.githubusercontent.com/103064444/174410298-8c076531-6873-4174-87c5-013519ff567a.png">

<img width="697" alt="Screen Shot 2022-06-17 at 6 53 11 PM" src="https://user-images.githubusercontent.com/103064444/174410316-3b76f016-c68c-4fdb-8809-243f08319264.png">

<img width="691" alt="Screen Shot 2022-06-17 at 6 53 02 PM" src="https://user-images.githubusercontent.com/103064444/174410325-71f5a0c2-9475-4c18-a1a2-7cd50dffe155.png">

<img width="690" alt="Screen Shot 2022-06-17 at 6 52 33 PM" src="https://user-images.githubusercontent.com/103064444/174410335-51be6669-a69f-4903-a6ac-64e80cc2c06e.png">

<img width="698" alt="Screen Shot 2022-06-17 at 6 52 09 PM" src="https://user-images.githubusercontent.com/103064444/174410351-0a3748ed-d6fe-4073-a509-75dd0b9ca7c6.png">

<img width="693" alt="Screen Shot 2022-06-17 at 6 52 42 PM" src="https://user-images.githubusercontent.com/103064444/174410361-74f31a3f-ae92-4204-9ab5-530c3a47ba90.png">

<img width="693" alt="Screen Shot 2022-06-17 at 6 52 51 PM" src="https://user-images.githubusercontent.com/103064444/174410365-8c48c735-2585-48d8-83a9-5f16500c75a3.png">

<img width="692" alt="Screen Shot 2022-06-17 at 6 52 19 PM" src="https://user-images.githubusercontent.com/103064444/174410388-f2991ac1-ead3-4d08-b823-ee08bdf7c44f.png">

<img width="691" alt="Screen Shot 2022-06-17 at 6 53 27 PM" src="https://user-images.githubusercontent.com/103064444/174410397-7f1fc4cf-a994-4bd3-a4fe-73d7dae131db.png">

From the boxplot for education level and target variable y, the ensembled plots show that if the education level of clients is illterate, target variable y is "no" for all the outcomes. Also, if the client does have credit in default, the client will also not subscribe the term deposit. The rest of the categorical variables show even distributions of "yes" and "no" in categories

### Modeling

#### Logistic Regression

Data has been splitted into train and test data, and the result shows that a decrease in employment varation rate will increase the chance of client subscribing a term deposit by 0.39. If the outcome of previous marketing campaign changed from failure to nonexistence, the chance of client subscribing a term deposit by 0.8, and if the previous marketing campaign outcome changes to success, the chance will then increase by 1.86. 

The result of the logistic regression has F1 score being 0.3209, with sensitivity 0.7384 and specificity 0.6862. The prediction accuracy is 0.7324 

#### Classification Tree

Grid search has been performed to find the hyperparameters for classification tree. The best F1 score has been found to be 0.7179 with cost penalty being 0.031 and minimum leaf to split being 1. The confusion matrix of the training set shows an accuracy of 0.7079, along with 0.7188 sensitivity and 0.6970 specificity. The confusion matrix of the validation sets shows an accuracy of 0.7221, with a 0.7233 sensitivity and 0.7128 specificty. The training sets and validation sets show similar prediction accuracy, meaning there is no overfitting problem in the classification tree model

<img width="694" alt="Screen Shot 2022-07-02 at 1 22 47 PM" src="https://user-images.githubusercontent.com/103064444/177010300-0d64fdd2-b647-4ca6-ade9-3b4a2b86456e.png">

#### Random Forest

Grid search has been performed to find the hyperparameters for random forest. The best F1 score is 0.6731 with ntree = 500 and mtry = 1. The confusion matrix of validation set shows an accuracy of 0.8465, which has an 17% increase from the classification model, and the sensitiviy is 0.8870 and specificty is 0.5319. 

<img width="690" alt="Screen Shot 2022-07-02 at 1 28 28 PM" src="https://user-images.githubusercontent.com/103064444/177010486-8b941880-7ba1-4950-b913-8ebf551bd3bf.png">

#### Boosted Tree

Grid search has been performed to find the hyperparameters for boosted tree. The best F1 score is 0.7051 with mfinal = 11. The confusion matrix shows an accuracy of 0.8028, which increases by 11% from the classification tree model, whereas lower than the random forest model. The sensitivity is 0.8288 and the specificity is 0.6011.

<img width="694" alt="Screen Shot 2022-07-02 at 1 34 42 PM" src="https://user-images.githubusercontent.com/103064444/177010652-3bc3f55b-8b43-4086-a084-cbb8b0aca5cd.png">

### Summary

After balancing the data by over sampling, classification tree model has the highest F1 score of 0.7179, which has improved by 123% from the logistic regression, but the prediction accuracy for classification tree is 0.7221, which is lower than the logistic regression's 0.7324. Random Forest, on the other hand, has a higher accuracy of 0.8465 than the classification tree model, with a higher sensitivity value and lower specificity value, meaning the random forest model will predict few false negative and more false positive results, comparing with the classification tree model. The boosted tree has increased F1 score by 4.8% from the random forest, but the accuracy is lower, with a lower sensitivity and higher specificity. Both the random forest and boosted tree perform better than the logistic regression and classification tree in terms of prediction accuracy.

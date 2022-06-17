# Data Science Project :: Bank-Marketing-Campaign

### Data

Data is collected from [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing#)

The data is related with direct marketing campaigns of a Portuguese banking institution. The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required, in order to access if the product (bank term deposit) would be ('yes') or not ('no') subscribed.

The classification goal is to predict if the client will subscribe (yes/no) a term deposit (variable y).

There are four datasests available from the data base, bank-additional-full.csv has 41188 observations and 20 inputs from 2008 - 2010, bank-additional.csv has 10% of the examples (4119) and 20 inputs, bank-full.csv all examples and 17 inputs, which is an older vesion of the data that has less inputs, and bank.csv has 10% of the examples and 17 inputs.

The dataset used for modeling and prediction is the bank-additional.csv, as it contains the newest inputs for measuring. All the categorical variables have been encoded as numbers for classification, and several variables are dropped due to insignificance.

### Exploratory Data Analysis

Numeric predictor variables:

<img width="694" alt="Screen Shot 2022-06-17 at 6 38 28 PM" src="https://user-images.githubusercontent.com/103064444/174410094-6992f1ec-89f9-413c-906d-4a825234976b.png">

Note: variable pdays originally has 999 meaning client was not previously contacted, and it has been changed to -1.

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

### Modeling

#### Logistic Regression

Data has been splitted into train and test data, and the result shows that a decrease in employment varation rate will increase the chance of client subscribing a term deposit by 0.39. If the outcome of previous marketing campaign changed from failure to nonexistence, the chance of client subscribing a term deposit by 0.8, and if the previous marketing campaign outcome changes to success, the chance will then increase by 1.86. 

The result of the logistic regression has F1 score being 0.321, with sensitivity 0.9911 and specificity 0.1915. 

#### Classification Tree

Grid search has been performed to find the hyperparameters for classification tree. The best F1 score has been found to be 0.501 with cost penalty being 0.001 and minimum leaf to split being 1.

<img width="695" alt="Screen Shot 2022-06-17 at 7 30 39 PM" src="https://user-images.githubusercontent.com/103064444/174412456-c75abe98-8ce1-463c-a786-5a95d2833df8.png">

#### Random Forest

Grid search has been performed to find the hyperparameters for random forest. The best F1 score is 0.44 with ntree = 100 and mtry = 7.

<img width="686" alt="Screen Shot 2022-06-17 at 7 30 19 PM" src="https://user-images.githubusercontent.com/103064444/174412448-2f48a894-5394-4e3e-a623-ab3ed4b49af3.png">

#### Boosted Tree

Grid search has been performed to find the hyperparameters for boosted tree. The best F1 score is 0.469 with mfinal = 71.

<img width="680" alt="Screen Shot 2022-06-17 at 7 31 05 PM" src="https://user-images.githubusercontent.com/103064444/174412446-72e61a3b-93bd-4d9c-aa27-6fffba7a77e4.png">


---
title:  "Bertelsmann"
subtitle: "To be or not to be a customer. That is the question"
author: "Dirk Lindner"
avatar: "img/authors/Bild_Dirk_Lindner.jpg"
image: "img/d.jpg"
date:   2023-03-31
---

### Customer Segmentation and Acquisition - Bertelsmann Arvato
In this project, I have employed the use of supervised and unsupervised machine learning algorithms to deal with real-life data provided by Bertelsmann Arvato Analytics. More specifically, I have worked on 4 demographics datasets and 2 metadata files provided by Arvato Financial Services with the goal of helping a client mailorder company target next probable customers.

### Github Repo:
You can find the full code here: https://github.com/dirkules339/Bertelsmann-Arvato-Project.git

### 1. Preprosessing
After a first look into the data I saw that the datasets included a lot of missing values. To clean the data enough without loosing to much data I decided to define a threshold for columns and rows to drop. By Using the confidence interval of 99% I defind the threshold for columns to drop by 20% missing values and for rows to drop by 10% missing values. By that I could keep 99% of columns and rows.

#### Proportion of missing values in AZDIAS features
![A test image](img/B1.png)

#### Proportion of missing values per row in AZDIAS
![A test image](img/B2.png)


Next I reencoded categorical variables and changed value errors to nan values with the help of some basic data manipulations and sklearns one hot encoder before I imputed missing values and scaled the features as preperation for the segmentation and modelling part.

#### Data manipulation 
![A test image](img/B3.png)

#### One hot encoded features
![A test image](img/B4.png)

#### Impute missing values
![A test image](img/B6.png)

#### Scale Features
![A test image](img/B7.png)


### 2. Customer Segmentation Report

For the customer segmentation I decided to do a PCA to reduce dimensions befor I use k-means clustering to to the customer segmentation. I wanted to keep a smaller number of features while retaining high explained data variance. To decide how many top components to include, it was helpful to look at how much data variance the components captured. Round about 210 features can explain 90% data variance. So I decided to keep 210 features for the segmentation.
 
#### Explained variance by principal components (AZDIAS)
![A test image](img/B8.png)

Next I did the segmentation with k-means clustering. At first I chose the numbers of clusters (10 clusters) with the help of an elbow graph. And after that I plotted the results of k-means clustering for the general population and the customer base. The plot shows that some clusters are overrepresented by customers (0, 1, 3, 6) whereas others don't. This gives us an idea of better targetting future customers.

#### Elbow graph
![A test image](img/B9.png)

#### General population and customer base in cluster
![A test image](img/B10.png)


### 3. Supervised Learning Model

In the last step I wanted to train and test a supervised learning model to predict whether an individual of the poulation is likely to become a customer. For that I looked into the train and test data likewise the data from step 1. I found out that there was an imbalance of the responses of the dataset so I needed to balance the data before I did the preprocessing likewise step 1. 

#### Balance train data
![A test image](img/B11.png)

I decided to use three different models for the prediction and compare them by their performances. I compared logistic regression, gradient boosting and lightgbm. Lightgbm had by far the best performance. But with an AUROC of 0.98 this could be a sign of overfitting. So I decided to go with the second best model gradient boosting (AUROC score of 0.9) for the prediction despite of the much more time taken by training the model.

#### Model performance
![A test image](img/B12.png)

Using the model on the test data I got a result of 9371 individuals likely to become a customer. Which are round about 21% of all test individuals.

#### Prediction
![A test image](img/B13.png)


### 3. Conclusion

So you can see it is very important to prepare the data used to get good results and it helps to have some generel knowledge of the data to identify issues. By using thresholds and imputing values it was possible to use as many data as possible to strongen the prediciton. 
Additionally it is a good idea to compare different models by there performance. I chose a model with a good performance over a model with less time taken by the training, but in some situations a really fast model is needed so it could be importent to take the time into account.
Overall the result seems to be a good model.



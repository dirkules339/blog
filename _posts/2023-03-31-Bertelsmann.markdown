---
title:  "Bertelsmann"
subtitle: "To be or not to be a customer. That is the question"
author: "Dirk Lindner"
avatar: "img/authors/Bild_Dirk_Lindner.jpg"
image: "img/d.jpg"
date:   2023-03-31
---

### 1. High Level Overview - Customer Segmentation and Acquisition - Bertelsmann Arvato
In this project, I have employed the use of supervised and unsupervised machine learning algorithms to deal with real-life data provided by Bertelsmann Arvato Analytics. Arvato is looking to determine which people would be the most likely to turn into customers. 

— Description of Input Data —

They have provided a few datasets:
 - Azdias (891221 rows, 366 columns): The Azdias dataset contains information on the general population.
 - Customers (191652 rows, 369 columns): The Customers dataset contains information on existing customers.
 - Mailout Train (42962 rows, 367 columns): The Mailout Train dataset contains data that describes customers that have either responded or not.
 - Mailout Test (): The Mailout Test dataset contains data that describes potential customers.

— Strategy for solving the problem—

The goal of the project is to predict whether or not the customers in the Mailout Test dataset will respond. In order to accomplish that, there are four main parts to the project:

Getting to Know the Data:
 - In getting to know the data, the Azdias and Customers datasets that contain the information about the general population and the customers will be processed and distilled down to the rows and columns that have data and are unique in their correlations.

Customer Segmentation:
 - The segmentation is to find similarities and differences between the general population and the known customers. The goal is to identify likely customers in the general population. This will be done using unsupervised learning techniques like PCA and KMeans.
 - Principal component analysis (PCA) will be used for dimensionality reduction. Then, in preparation for the KMeans algorithm, clustering through the use of an elbow curve will be used.
 - The KMeans algorithm will be used to make sense of the clusters and figure out which of those clusters make the most difference in determining the likelihood of a person turning into a customer.

Supervised Learning Model:
 - By building a machine learning model using the Mailout Train dataset, with the response of a marketing campaign, the determination can be made for which people are most likely to become customers.
 - I use several machine learning classifiers and then choose the best using analysis from learning curves. This model can then be used to make predictions

— Metrics —

 - An AUC-ROC curve from predicted probabilities will be used to evaluate the performance of the models.
 - AUC-ROCis a performance measurement for the classification problems at various threshold settings. ROC is a probability curve and AUC represents the degree or measure of separability. It tells how much the model is capable of distinguishing between classes. Higher the AUC, the better the model is at predicting whether a person is just a person or if they are really a customer.
 - ROC is created by plotting the true positive rate (TPR) against the false positive rate (FPR).

### 2. Data Exploration and Preprosessing
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


### 3. Customer Segmentation Report

For the customer segmentation I decided to do a PCA to reduce dimensions befor I use k-means clustering to to the customer segmentation. I wanted to keep a smaller number of features while retaining high explained data variance. To decide how many top components to include, it was helpful to look at how much data variance the components captured. Round about 210 features can explain 90% data variance. So I decided to keep 210 features for the segmentation.
 
#### Explained variance by principal components (AZDIAS)
![A test image](img/B8.png)

Next I did the segmentation with k-means clustering. At first I chose the numbers of clusters (10 clusters) with the help of an elbow graph. And after that I plotted the results of k-means clustering for the general population and the customer base. The plot shows that some clusters are overrepresented by customers (0, 1, 3, 6) whereas others don't. This gives us an idea of better targetting future customers.

#### Elbow graph
![A test image](img/B9.png)

#### General population and customer base in cluster
![A test image](img/B10.png)


### 4. Supervised Learning Model

— Balance the train data —

In the last step I wanted to train and test a supervised learning model to predict whether an individual of the poulation is likely to become a customer. For that I looked into the train and test data likewise the data from step 1. I found out that there was an imbalance of the responses of the dataset so I needed to balance the data before I did the preprocessing likewise step 1. 

#### Balance train data
![A test image](img/B11.png)

— Modeling and Tuning —

I decided to use three different models for the prediction and compare them by their performances. I compared logistic regression, gradient boosting and lightgbm. Lightgbm had by far the best performance. But with an AUROC of 0.98 this could be a sign of overfitting. So I decided to go with the second best model gradient boosting (AUROC score of 0.9) to tune in the next step. The tuning didn't really change the results but was pretty good in the first place.

#### Model performance
![A test image](img/B12.png)

#### Model performance
![A test image](img/B14.png)

— Results and Justification —

The final AUROC score of the project is 0.9. What seems to be a really good result which shows that the goal of the project was achieved. 
Using the model on the test data 9371 individuals are likely to become a customer. Which are round about 21% of all test individuals.

In the building of the supervised learning model, during the preprocessing phase, there were many columns that were used, but there were also many columns that were removed. When looking at the threshold to use for removing columns and rows with null data, it was determined to remove columns that have 40% and rows that have 10% or more missing data. This value could easily have been changed up or down and would have an effect on the final model.



#### Prediction
![A test image](img/B13.png)


### 5. Conclusion and Improvement

So you can see it is very important to prepare the data used to get good results and it helps to have some generel knowledge of the data to identify issues. By using thresholds and imputing values it was possible to use as many data as possible to strongen the prediciton. 
Additionally it is a good idea to compare different models by there performance. I chose a model with a good performance over a model with less time taken by the training, but in some situations a really fast model is needed so it could be importent to take the time into account.
Overall the result seems to be a good model.

However, this project is not complete. There is much more work that could be done on the data to improve the predictive model. For instance, more or fewer features could be removed. The taken time for model training was really high (Time taken: 597.1155662536621) so maybe it would be better to test other algorithms as well like random forest. And Lightgbm had a really good model AUROC score of .98 where I assumed overfitting issue, so it is woth looking into that and find out if that is true.

### Github Repo:
You can find the full code here: https://github.com/dirkules339/Bertelsmann-Arvato-Project.git

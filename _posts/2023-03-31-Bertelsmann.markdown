---
title:  "Bertelsmann"
subtitle: "To be or not to be a customer. That is the question"
author: "Dirk Lindner"
avatar: "img/authors/Bild_Dirk_Lindner.jpg"
image: "img/ball.jpg"
date:   2023-03-31
---

### Customer Segmentation and Acquisition - Bertelsmann Arvato
In this project, I have employed the use of supervised and unsupervised machine learning algorithms to deal with real-life data provided by Bertelsmann Arvato Analytics. More specifically, I have worked on 4 demographics datasets and 2 metadata files provided by Arvato Financial Services with the goal of helping a client mailorder company target next probable customers.

### Github Repo:
You can find the full code here: [https://github.com/dirkules339/Bertelsmann-Arvato-Project.git]

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


### 2. Simple linear regression model to predict market value of players

After getting a better understandig of the data I generated dummy variables as preparation for a first linear regression model to predict the market value of soccer players. Below you can see the example of sub postion dummy variables. For the regression model I generated dummy variables of postion, sub postion, foot and the current competition id. Additionally I used current club id and the players heights as variables for the model.
 
#### Generate dummy variables of sub positions (basic information)
![A test image](img/6.png)

With a training R2 of 0.25 the first model wasn't quiet good. You can see how predicted and actuel response differ in the plot below. Interessting fact: The testing R2 of scikit learn linear regression model becomes negative if it is lower than 0.5! 

#### Compare prediciton with actual response
![A test image](img/7.png)

To improve the model I added additional variables like goals, assists, red cards, yellow cards and minutes played to our dataset. Even if that improved the training R2 to 0.55 the testing R2 is still negative. That means the model has still room for improvement, but by adding some more specififc player stats to the model I easily doubled the fit. 

#### Generate dummy variables (personal player stats)
![A test image](img/8.png)

#### Compare prediciton with actual response
![A test image](img/9.png)

### 3. Conclusion

So you can see it is very easy to get a simple prediciton model running in the firs place. But it is very important to prepare the data used to get good results and it helps to have some generel knowledge of the data to identify issues. For me as soccer fan for example it was easy to see that something was wrong with my dataset as I saw the rank of nehterlands soccer league. Aside from that it is really important to use the right variables to get good model fit. You should onl use these ones who have an actua impact on your dependent variable.



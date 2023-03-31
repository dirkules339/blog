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

### 1. Take a look at the data
After I took a first Look on the data with a the help of a boxplot, I saw that there are some changes needed befor the data is interpretable. So I changed the format of the market value into million € to make it more readable. I only included data where the market value is not null and the players last season where in 2022 and they haven't got an expired contract right now. I did that to look only at players who are still playing in an european pro league.

#### Market value compared by league (first try)
![A test image](img/1.png)

#### Market value compared by league (second try)
![A test image](img/2.png)


Nexts things I looke into where the top ten clubs by players market value and the top ten players. Six clubs of the top 10 are from great britain. The other four clubs are from Spain, Germany and France and again not from Italy, despite Italy is ranked number three of Leagues by players market value. You can see something quit similar in the top ten of players. Four players are from Great Britain, followed by Spain with three, Germany with two and France with one player and again Italy is not ranked with players within the top ten. In addition you can seet that there are no defenders within the top ten and that the market value of players differs within the player positions. So maybe this infromation helps to predict the market value of players. That is what I looked into int the second part. 

#### Top 10 Clubs by players market value 
![A test image](img/3.png)

#### Top 10 Players by market value
![A test image](img/4.png)

#### Market value by sub position
![A test image](img/5.png)


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



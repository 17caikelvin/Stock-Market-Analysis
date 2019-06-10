Stock Analysis Data Science Project
===================
In this write-up, I will detail the why, what, and how of my analysis on the stock of a variety of tech companies. I used information pulled from Yahoo and Google to visualize different aspects of stock information, then analyzed each stock's risk, and lastly predicted future stock prices with a Monte Carlo method. 

Below, I will recap my thought process and the steps I took towards my goal. 


----------

Data Requesting and Description
-------------
I first used *pandas*, an online software library for data manipulation in Python, to request stock information from Yahoo. I requested data from Apple, Google, Microsoft, and Amazon. After setting time parameters for one year prior and today, I could come up with a description of the data. The information I was given included: Opening price, the highest and lowest price, closing price, volume, and adjusted closing price. 


----------


Observations and Analysis
-------------------
For the visualization of aspects of stock information, I chose to only analyze Apple, because analyzing all four of the companies I had in mind would make it hard to read and was largely unnecessary with my goal in mind. I started by plotting 
**Observations**:
1. Apple's closing prices experienced a significant decline in price starting from November 2018 and ending in January 2019. The price has since rebounded to about half of its previous peak, but is starting to decline again. 
2.  The volume of Apple stock spiked dramatically around the same time that it hit its lowest point in price.
3.  The stock's moving average followed the same trend as its price.
4.  Daily return was most variant while the stock was declining, then stabled out as it reached its lowest point and started rebounding. 

After looking at all these variables, I moved onto comparing the daily returns of each company against each other. Interestingly enough, all the companies' daily returns seemed relatively correlated to each other. The most tightly related were between Amazon and Microsoft, and Amazon and Apple. 



----------


Analyzing Risk
-------------
I first used the "bootstrap" method to analyze risk. This entails calculating empirical quantiles from a histogram of daily returns. After plotting the histogram, I calculated the 0.05 empirical quantile of daily returns, which came out to -0.03123. This means that with 95% confidence, our worst daily loss will not exceed 3.123%. 

I then used the Monte Carlo method to run many trials with random market conditions, and then calculate portfolio losses for each trial. After implementing my function, I came up with a model 
After analyzing all the variables that were given to me, it was time to create a model based on what I learned. 

**Combining features into new features**
Because of the similarity between Parch and SibSP, I decided to combine them into one "Size of family" variable that would allow for a more robust model with less variables. After analyzing this new variable, however, I realized it would be best to instead create a "IsAlone" variable that would allow me to forgo Parch, SibSp, and SizeOfFamily. I also decided to combine Age and Class by multiplying the values together.

**Converting features into numerical values**
Because some variables had non-numerical values, it was necessary for them to be converted in order to fit the model. Gender was easy to change, and I simply made Female values 0 and Male values 1. Age was separated into bands, or groups, and given ordinal values with 0 being children and 4 being elders. Fare was also split into bands in a similar fashion as Age. I derived titles from each passenger's name, grouping them into Mr., Miss, Mrs. Master, and Rare as a blanket label for people that did not fit any of the other labels. These were also given ordinal values from 0-4. IsAlone was already a binary value, and Age*Class was numerical as well. Now that all of our variables were able to be fit into our model, it was simply a matter of using them to create different models.

**Modeling**
I split the training file into X_train and Y_Train, using all columns except the variable Survived for X_train, and only Survived for Y_train. X_test was derived from the testing file with PassengerID dropped. From here, it was only a matter of using imported types of predictive modeling algorithms. The models I used included: Logistic Regression, k-Nearest Neighbors, Support Vector Machines, Naive Bayes classifier, Decision Tree, Random Forest, Perceptron, Artificial neural network, and Relevance Vector Machine. 

After running all models and recording their confidence scores, I found that the Random Forest and Decision Tree models were the most accurate, with both of them tying with 86.76% confidence scores.

**Conclusion**
Thus concludes my first data science project. I was able to implement what I have learned so far by analyzing the task and data at hand, analyzing said data and verifying various hypotheses, cleaning and modeling significant variables with different modeling techniques, and ultimately creating a model with about 87% accuracy. 

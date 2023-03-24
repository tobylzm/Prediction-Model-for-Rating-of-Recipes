# Prediction-Model-for-Rating-of-Recipes

This is a project for DSC 80 at UCSD

by Zhiming Liu (zhl109@ucsd.edu)

Our exploratory data analysis on this dataset can be found [here] (https://tobylzm.github.io/Healthy-High-Protein-Recipes/)

---

## Framing the Problem
### Prediction Problem: Predict the average rating of recipes

This is a classification type of prediction since the value of average rating is ordinal discrete. I choose average rating because it is the best reflection of the quality of recipes and give a good sense of if I will like the recipes. Also, I choose accuracy as my metric to evaluate the model, becasue the consequence of false negative and false positive is quite the same.

---

## Baseline Model

I use the K Nearest Neighbour Classifier as the model prediction. A k-Nearest Neighbors (k-NN) regressor predicts the response value of a (new) observation by computing the average value of the k-closest observations in the training set. (quote from lab 9)I pick three fectures: minutes(quantitative),cal_pro_ratio(quantitative) and is_vegetarian(categorical,nominal). I use train test split to split my model. This way it can have a better ability to generize unseen data. Before fitting my model, I did some processing to my data. I leave the minutes as is. I use binerizer to binerize cal_pro_ratio, the reasons I did that is that I want to the model to distinguish whether the food is a healthy high protein food (the analysis I did in project 3). I use one hot encoder to encode the is_vegetarian featurem, since it is a categorical feature. The performance of the model is having around 60 percent of accuracy. This is not good, because 5 star rating have more about 57 percent in the dataset. That means my model should at least be 57 percent of accuracy. Mine is only 3 percent higher than it.

---

## Final Model

I added three new features n_ingredients,n_steps and tags.
n_steps and n_ingredients features represents the complexity of the recipes, so it could have affected cooker expreience, thus affected their rating
I deal with the tags feature using count vectorizer. Too much features would slow down the model and take too long to predict. So I use max features=10 to limit the features amount. The tags build some first impression on the cooker. So it may affect their rating for the over all recipes.

I still choose K Nearest Neighbours, since it is not bad when implementing the baseline model
Then I use GridSearchCV, with cross validation of 5. After searching, I found the best parameter is .I use that parameter to implement
The model acuuracy improve by 10 percent. The reason it improve is because more features are added, and a grid search is applied to find the best hyper parameter for the best under 5-fold validation.

---

## Fairness Analysis

My choice of Group X: Food that is not vegetarian
My choice of Group Y: Food that is vegetarian

Null hypothesis: The classifier's accuracy is the same for non-vegetarian food and vegetarian food, and any differences are due to chance.
Alternative Hypothesis: The classifier's accuracy is not the same for non-vegetarian food and vegetarian food

Choice of statistic: absolute difference in accuracy
Significance leve: 0.05

The resulting p-value: 0.89
Conclusion: Fail to reject that the classifier's accuracy is the same for non-vegetarian food and vegetarian food.




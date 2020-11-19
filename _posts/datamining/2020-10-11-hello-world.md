---
layout: post
title: "Ensemble Methods!"
read: 15
secondary: datamining
date: 2020-11-18
---

## Ensemble methods

*Terminlogies:* 

+ "Model" is used to describe the output of the algorithm that trained with data

+ Algorithm is any machine learning algorithm (e.g, logistic regression, decision tree...). These models are used as inputs of ensemble methods that are called "base models"

1. Why do we need ensemble methods ?
   
Main causes of error in learning is: noise, bias and variance

-> Ensemble is designed to improve stability and accuracy of machine learning algorithms

-> We need to train multiple models using same base models

-> Then, combine multiple classifiers to decrease variance and increase reliability of classification than using a single classifier. 

2. General rule of using ensemble method

Select a base learner algorithm (e.g Decision tree), then ensemble method creates many as trees as it wants by generating additional data randomly with replacement (meaning that size of training data does not change, but some observations may be repeated many times in each new training dataset)

3. Ensemble methods

Some widely known methods of ensemble: voting, stacking, bagging and boosting

**Voting**

+ Voting: is used for classification
    + Majority voting: every model makes a prediction (votes) for each test instance and the final output prediction is the one that receives more than half of the votes
    + Weighted voting: we can increase the importance of one of more models
+ Averaging: is used for regression
  + Simple averaging: the average predictions are calculated. This method reduces overfit and creates a smoother regression model.
  + Weighted averaging: prediction of each model is multiplied by the weight and then their average is calculated.

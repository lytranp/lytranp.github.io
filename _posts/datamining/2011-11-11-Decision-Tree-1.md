---
layout: post
mathjax: true
title: "Decision Tree - Part 1"
read: 15
secondary: datamining
date: 2020-11-18
---

### 1. Introduction

![](/sources/datamining-decision-tree-1.png){:height="60%" width="60%"}

**Interpretation**

+ Classify target variable with 3 levels: setosa, versicolor, virginica
  
+ A node's gini measures its impurity: a node is pure (gini = 0) if all training instances it applies to belong to the same class

Root node: length <= 2.45

Depth-1:
+ Left node: There are 50 training instances with length <= 2.45
  
  + Among 50 these training instances, all are setosa => pure => gini =0
  
  + Value = [50,0,0]: 50 are setosa, 0 versicolor, 0 virginica
  
+ Right node: 

  + Value = [0,50,50]: 0 are setosa, 50 versicolor, 50 virginica => continue splitting
  
Depth-2 left:

+ Left node: There are 54 training instances with width <= 1.75
  
  + Gini = 1 - (0/54)^2 - (49/54)^2 - (5/54)^2 = 0.168
  
+ Right node: There are 46 training instances with width > 1.75

### 2. Decision Tree decision boundaries

- The lefthand area is pure (only setosa), it can not splits any further
  
- Righthand area is impure, so depth-1 right node splits at width = 1.75 (represented by dashed line)
  
- If set max_depth = 2, Decision trees stops right there.
  
- If set max_depth = 3, two depth-2 nodes would add another decision boundary (represented by dotted line)
  
![](/sources/datamining-decision-tree-2.png){:height="60%" width="60%"}

### 3. Estimate Class Probabilities 

Assume we stop at depth-2 right node, so Decision Tree should out the following probabilities: Value = [0,49,45]: 0% for setosa (0/54); 90.7% for versicolor (49/54) and 9.3% for virginica 

=> If predict class with attributes: length > 5 and width < 1.75, then it will be versicolor class because it has the highest probability

![](/sources/datamining-decision-tree-3.png){:height="40%" width="40%"}

### 4. CART algorithm

Scikit-learn uses CART (Classification and Regression Tree) algorithm to train Decision Trees. The algorithm works by first splitting the training set into 2 subsets using a single feature k (length) and a threshold t (<= 2.45) at that feature k. 

How to choose k and t ? Use CART cost function for classification. Once CART algorithm successfully split the training set in two, it splits the subsets using the same logic, then the sub-subsets, and so on. It stops recursing once it reaches the maximum depth (*max_depth* hyperparameter), or if it can not find a split that will reduce impurity. To see example, please read [Decision Tree - Part 2](2011-11-11-Decision-Tree.md)

![](/sources/datamining-decision-tree-4.png){:height="60%" width="60%"}

**Conclusion**

+ Use CART algorithm to choose splitting value (by comparing GINI final at each node) as [Decision Tree - Part 2](2011-11-11-Decision-Tree.md)
  
+ After having splitting value, we can compute GINI in each node to know if it is pure node and estimate class probability to see what class instance belongs to if stop there. 

### 5. Regularization hypeparameters

+ Non-parametric model (Decision Trees): make very few assumptions about training data, many parameters are not determined prior to training => model structure is free to stick closely to the data => it fits very closely, most likely overfitting. 
  
+ Parametric model (Linear models): have assumption that data is linear, has pre-determined number of parameters => its degree of freedom is limited => reduce risk of overfitting

To avoid overfitting the training data, we need to restrict Decision Tree's freedom during training: called regularization. Regularization hyperparameters depend on the algorithm used. 

Some common hyperparameters for Decision Tree
+ max_depth: default is None, means unlimited
  
+ min_samples_split: the minimum number of samples a node must have before it can be split

+ min_samples_leaf: the minimum number of samples a leaf node must have 
  
+ max_leaf_nodes: maximum number of leaf nodes
  
+ max_features: maximum number of features that are evaluated for splitting at each node

### 6. Compare Decision Tree with classification and regression tasks

There are 2 main difference

- Instead of predicting class in each node, it predicts a value
  
- Instead of trying to split the training set to minimize impurity, it tries to split to minimize MSE (Below formula of MSE node implies that it expects values in a node are nearly equal)

![](/sources/datamining-decision-tree-5.png){:height="60%" width="60%"}

![](/sources/datamining-decision-tree-6.png){:height="60%" width="60%"}

### 7. Main limitation of Decision Trees

Very sensitive to small variations in the training data. For example, just after removing 1 instance with biggest width, and train a new Decision Tree, we may get new model

*Before removing 1 instance*

![](/sources/datamining-decision-tree-2.png){:height="60%" width="60%"}

*After removing 1 instance*

![](/sources/datamining-decision-tree-7.png){:height="60%" width="60%"}

------------------
**References**

Aurelien Geron, Hands-on Machine Learning with Scikit-Learn, Kera & TensorFlow


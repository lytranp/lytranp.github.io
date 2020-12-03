---
layout: post
mathjax: true
title: "Neural Networks - From perspective of deep learning "
read: 15
secondary: datamining
date: 2020-11-18
---
*This post was written to reflect what I read in the book "Data mining for Business Analytics Concepts"*

### 1. Introduction

This picture describes very well about neural network. We will learn more about Math behind Neural Network

![](/sources/neural-networks-1-1.png){:height="60%" width="60%"}

Neural networks are models for classification and prediction; also can used for unsupervised tasks such as feature extraction.

### 2. Tiny example
**Terminlogies:**

- Input layer consists of nodes (sometimes called neurons) that simply accept the predictor values 

- Successive layers of nodes receive input from the previous layers.

- Outputs of nodes in each layer are inputs to nodes in the next layer

- Last layer is called the output layer

- Layers between the input and output layers: hidden layers

**Problem**: Based on tasting score of 6 consumers to predict their preference

![](/sources/neural-networks-1-2.png){:height="40%" width="40%"}

![](/sources/neural-networks-1-3.png){:height="60%" width="60%"}

*Interpretation*

- Nodes N1, N2: belong to input layer. Input nodes are values of predictors. If we have p predictors, input layer often include p nodes. 
  
  - In our example: includes 2 nodes
  
  => input layer is Fat = 0.2; Salt = 0.9 

  => output of this layer is: $x_1$ = 0.2 and $x_2$ = 0.9

- Nodes N3, N4, N5: belong to hidden layer

  - In our example: hidden layer consists of 3 nodes, each receiving input from all input nodes.

  - To compute output of a hidden layer node: compute a weighted sum of inputs and apply a certain function to it. 

  - Weighted sum: 
    
    s = $\hat{\theta}_j$ + $\displaystyle\sum_{i=1}^p(w_i,_j)$
    
    Because there are p predictors, i will run from 1 to p. 
    
    $w_1,_j,...w_p,j$ are weights that are **initially sets randomly**. $\hat{\theta}$ is also called the bias of node j, is a constant that controls the level of contribution of node j.

  - Next, we take a function g of this weighted sum. Function g is called a transfer function or activation function. Functions might include: linear function [g(s) = $\hat{\theta}$s], exponetial function [g(s) = exp($\hat{\theta}$s)], logistic/sigmoidal function [g(s) = $\frac{1}{1+e^-s}$]

  - If we choose logistic activation function, the output of node j in the hidden layer is

    ![](/sources/neural-networks-1-4.png){:height="60%" width="60%"}

  - $\hat{\theta_j}$ and $w_i,_j$: assigned randomly in the first round of training, very small, around zero. Suppose that initial bias and weights for node N3 are: $\hat{\theta_3}$ = -0.3; $w_1,_3$ = 0.05; $w_2,_3$ = 0.01. Plug these numbers into logistic function, we can compute the output of node N3 in the hidden layer

![](/sources/neural-networks-1-5.png){:height="60%" width="60%"}

  - If there is more than one hidden layer, the same calculation applies, except that input values for the second, third, and so on, hidden layers would be the output of the preceding hidden layer.

  - Finally, the output layer contains input values from the last hidden layer. Then, it takes a weighted sum of its input values and applies the function g. In our example, output node N6 receives input from 3 hidden layer nodes. Output Node N6 is computed as below

![](/sources/neural-networks-1-6.png){:height="60%" width="60%"}

 - Use cutoff value 0.5, we would classify this record as *like*. For applications with more than 2 classes, we choose the output node with the largest value

- Node N6: belong to output layer

- Values on connecting arrows: weights 

- Weight on the arrow from node i to node j is denoted: $w_i,_j$
  
- Bias parameters inside each node: denoted by $\hat{\theta}_j$

### 3. Relation to Linear and Logistic Regression
a. Formulation

- If a neural network with no hidden layers and a single output node,then 
  
  $\hat{Y}$ = g(s) = $\hat{\theta}_j$ + $\displaystyle\sum_{i=1}^p(w_i,_j)$

This is exactly equivalent to the formulation of a multiple linear regression. 

- For a binary output variable Y, if g is logistic function, the output is:

![](/sources/neural-networks-1-7.png){:height="30%" width="30%"}

b. Estimation method

Training the model means estimating $\hat{\theta}_j$ and $w_i,_j$ (bias and weights) to have best predictive results. For each record, the model produces a prediction which is then compared with the actual outcome value. Its difference is the error.

Linear regression uses least square (sum of squared errors) and logistic regression uses maximum likelihood method to calculate coefficients. 

Neural network uses back propagation of error to update the estimated parameters (bias and weights)

### 4. Back propagation of error

Ordinary definition of an error = ($y_k$ - $\hat{y}_k$)

Error associated with output node k is compute by: ($y_k$ - $\hat{y}_k$) multiplied by a correction factor. 

![](/sources/neural-networks-1-8.png){:height="20%" width="20%"}

Then, bias and weights are updated as follows

![](/sources/neural-networks-1-9.png){:height="20%" width="20%"}

where l: learning rate (or weight decay parameter), ranging from 0 to 1, controls the amount of change in weights from one iteration to the next

*In our example*: The error associated with output node N6 **for the first record** is: (0.506)(1-0.506)(1-0.506) = 0.123. This error is then used to update the bias and weights using above formula. 

### 5. Update the bias and weights

There are 2 methods: 

+ *Case updating*: parameter values are updated after each record is run through the network. In our example, the error for the first record = 0.123. Using a learning rate of 0.5, we will update $\hat{\theta}$ and $w_i,_j$ to:

![](/sources/neural-networks-1-10.png){:height="30%" width="30%"}

These new values are next updated after the second record is run through the network, the third and so on, until all records are used. This is called one epoch. 

+ *Batch updating*: the entire training set is run through the network and the error $err_k$ is the sum of the errors from all records. After that, use this error to update the bias and weights as formula.

### 6. When does the updating stop ?

The most common conditions are one of the following:

- When new values of the bias and weights are only incrementally different from those of the preceding iteration

- When misclassification rate reaches a required threshold

- When the limit on the number of runs is reached

### 7. Avoid overfitting

Neural network can easily overfit the data, causing error rate on validation data to be large

=> Need to limit the number of training iterations

In classification and regression trees: overfitting can be detected by exammining the performance on validation set or better on a cross-validation set. When validation/cross-validation increases while training set performance is still improving, it is the sign of overfitting. Please read more [Bias-Variance-Detection](2020-11-21-Bias-Variance-Detection.md)

-----------
**References**

Galit Shmueli Peter, C.Bruce Peter Gedeck, Nitin R.Patel, Data Mining for Business Analytics Concepts, Techniques and Applications in Python
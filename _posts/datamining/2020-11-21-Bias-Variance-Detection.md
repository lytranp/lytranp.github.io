---
layout: post
title: "Bias & Variance - Detection!"
read: 15
secondary: datamining
date: 2020-11-21
---

## 1. Bias (Underfitting)

Models with high bias is known as underfitting: try to teach model to perform a task without presenting all of the necessary information. It is likely that you are not using enough features to train the model

## 2. Variance (Overfitting)

On the other extreme, model learns too much from training data, even capturing the noise in the data in addition to the signal. Model with high variance pays too much attention to the training data without considering for generalizing to new data. 

## 3. Trade-off of bias and variance

If we want low bias -> need to make model more complex to fits almost perfectly all the data points in the training set -> likely overfitting (high variance)

If we want low variance to avoid overly complex model -> likely that model is too simple and performs poorly on training data that extremely likely to repeat the poor performance on test data

=>We need to accept a trade-off. We can not have both low bias and low variance, so we want to aim for something in the middle.

![](/sources/Bias-Variance-Detection.png){:height="60%" width="60%"}


## 4. Common tools to diagnose high bias or high variance

### a. **Validation curve**

The parameters of model have some degree of control over the model's complexity (eg. degree of polynomial features)

-> Validation curve is a plot of the model's error as a function of some model hyperparameher which controls the model's tendency to overfit or underfit the data.

On this curve, we plot both training error and validation error of the model. 

![](/sources/Bias-Variance-Detection1.png){:height="60%" width="60%"}


>*Interpretation:* 

When parameter is small -> the error of model is high for both training and validation error. For example, in the 1st graph, regression model with degree = 1 -> underfit data. 

When parameter increased -> training error and validation error decreased although validation error must be larger than training error. The middle graph illustrated this. 

When parameter is really big (eg. degree = 10), the training error is low but the model does not generalize well (overfit) -> it performs poorly on new test data -> validation error increased. The last graph illustrated this. 

![](/sources/Bias-Variance-Detection2.png){:height="60%" width="60%"}

***Diagnose bias or variance from validation curve***

- In the region where both training error and validation error are high: model has high bias (underfitting) because the model can not learn from the data that leads to perform poorly
  
- In the middle region where both training error and validation error decrease: degree of parameter seems to be the best
  
- In the region where training error keeps staying low while validation error increases: it is effects of high variance (overfitting). Training error is low because the model is complex and it learns too much from training instances. But it can not generalize well to new data. As a result, validation error increases.


### b. **Learning curve**
We plot error of a model as function of number of training examples. We will plot the error for both the training data and validation data

![](/sources/Bias-Variance-Detection3.png){:height="60%" width="60%"}

Learning curve for linear regression 

![](/sources/Bias-Variance-Detection4.png){:height="60%" width="60%"}

>*Interpretation:* 

When size of training set is 1, MSE for training set is 0. This makes sense because model has no problem to train and fit perfectly a single data point. So, prediction on training set with size = 1 is perfect. However, using this trained model on 1 instance to predict validation set (which has 1999 instances), MSE is extremely high. This makes sense again because no way a model trained on a single data point can generalize accurately to 1999 new instances that it has not seen in training. 

=> When size of training set increase to 1000, the training MSE increases because it is hard to have a model predict accurately many instances. At the same time, because it trains on many instances, it can learn well and can predict well new data. Therefore, validation MSE decreases sharply. 

***Diagnose bias or variance from learning curve***

- If training error is very low: means that training data is fitted very well -> it has low bias and likely to be high variance.
  
- If training error is high: means that training data is not fitted well enough -> it has high bias and likely to be low variance

- If model has high bias: we will observe fairly quick convergence to a high error for both validation and training datasets. (Model has high training error -> high bias. At the same time, although validation error decreases when training set size increases, it does not keep decreasing any more. Validation error stays as high as training error, meaning that model can not predict well new datasets.)

![](/sources/Bias-Variance-Detection5.png){:height="60%" width="60%"}

![](/sources/Bias-Variance-Detection6.png){:height="60%" width="60%"}

- As we can see, from around 500 training data points onward, validation MSE stays roughly the same -> Adding more training data points won't lead to significantly better models. We should switch to an algorithm that can build more complex models or add more features to increase the complexity of current model. 

- Variance: examine gap between the validation learning curve and training learning curve: narrow gap indicates low variance; wider gap indicates higher variance. The reason is because if model fits training data too well -> training error will be low but validation error will be high -> gap between training and validation learning curve determines how high variance is
  
![](/sources/Bias-Variance-Detection7.png){:height="60%" width="60%"}

![](/sources/Bias-Variance-Detection8.png){:height="60%" width="60%"}

-------------
**Reference** 

https://www.jeremyjordan.me/evaluating-a-machine-learning-model/

https://www.dataquest.io/blog/learning-curves-machine-learning/
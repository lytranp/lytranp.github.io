---
layout: post
mathjax: true
title: "Model Evaluation - Part 2"
read: 15
secondary: datamining
date: 2020-12-05
---

Please read [Model Evaluation - Part 1](https://lytranp.github.io/notes/Model-Evaluation)

As we mentioned in Part 1, after using cross validation, we will have error at each iteration. But what is error ? How do we define error for different models ? How is error computed ? 

There is a various criteria by which model can be evaluated and compared. In general, Error (or called metric to assess mode performance) can be divided into two sections

- Classification Problem

    + Confusion Matrix

    + Gain and Lift charts

    + K-S chart

    + ROC chart / Area under the curve (AUC)

- Regression Problem 

    + Root Mean Squared Error (RMSE)

    + Relative Squared Error (RSE)

    + Relative Absolute Error (RAE)

    + Coefficient of Determination $R^2$

    + Standardized Residuals (Errors) Plot


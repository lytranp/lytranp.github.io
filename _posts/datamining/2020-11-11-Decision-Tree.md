---
layout: post
title: "Decision Tree - Gini Index!"
read: 5
secondary: datamining
date: 2020-11-21
---

1. Case study 

![](/sources/DataMining-DecisionTree.png)

2. At each node, we will see how well these candidates (Chest Pain, Weight) separate patients with heart disease (HD) and patients with no heart disease.

Question: How to know which candidate we will choose to do root node. If so, what splitting value we will choose ?

3. Solution

Step 1: Split data at each node

![](/sources/DataMining-DecisionTree2.png)

Weight

Because weight is numeric, we will use all of distinct values as splitting value. At each distinct value, we will compare <= 40; <= 50

![](/sources/DataMining-DecisionTree3.png)

![](/sources/DataMining-DecisionTree4.png)

Step 2: Evaluate splits
There are 3 populuar ways
- Use Logworth
- Use Gini impurity
- Use Entropy

We use these measurements to calculate for each node at different thresold, then compare among these nodes to select the best.

Example: Gini index for Chest Pain (2 levels: Yes & No)
 
 At each node, compute GINI leftside and Gini rightside, then compute final GINI index


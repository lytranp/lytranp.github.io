---
layout: post
title: "Decision Tree - Gini Index!"
read: 5
secondary: datamining
date: 2020-11-21
---

### 1. Case study 

![](/sources/DataMining-DecisionTree.png)

### 2. Choose candidate to split 

At each node, we will see how well these candidates (Chest Pain, Weight) separate patients with heart disease (HD) and patients with no heart disease.

Question: How to know which candidate we will choose to do root node. If so, what splitting value we will choose ?

### 3. Solution

**Step 1**: Split data at each node

![](/sources/DataMining-DecisionTree2.png)

![](/sources/DataMining-DecisionTree2.png)

Start with candidate "Weight": Because weight is numeric, we will use all of distinct values as splitting value. 

At each distinct value, we will compare <= 40; <= 50

![](/sources/DataMining-DecisionTree3.png)

![](/sources/DataMining-DecisionTree4.png)
=======
![](/sources/DataMining-DecisionTree3.png)

![](/sources/DataMining-DecisionTree4.png)

**Step 2**: Evaluate splits

There are 3 popular ways:
Use Logworth
Use Gini impurity
Use Entropy

We use these measurements to calculate for each node at different threshold, then compare among these nodes to select the best.
 
At each node, compute GINI left side and GINI right side, then compute final GINI index

$$ GINI = 1 - (P)^2 $$


 **Example**: GINI index for Chest Pain (2 levels: Yes & No)

 $$ GINI = 1 - (P)^2 
         = 1 - {P(Yes)^2 + P(No)^2} $$ 

At Chest Pain:

GINI left
$$ 1 - (\frac{2}{3})^2 - (\frac{1}{3})^2 = 0.44  $$

GINI right
$$ 1 - (\frac{1}{2})^2 - (\frac{1}{2})^2 = 0.5 $$

GINI final
        P(Left side) * GINI left + P(Right side) * GINI right 
where:  P(Left side) = P(YES OF CHEST PAIN ON ALL DATA) 

        P(Left side) = P(NO OF CHEST PAIN ON ALL DATA)
        
$$(\frac{3}{5}) * 0.44 + (\frac{2}{5}) * 0.5 = 0.47 $$

Similarly, we can compute GINI final for Weight at splitting values 40 and 50

**Step 3** Compare GINI final among candidates to find the LOWEST final GINI.

Example, GINI final of Chest Pain is the lowest, mean that although Chest Pain does not create pure leaves, it creates the least impurity.

**Step 4:** Let's say Chest Pain has the lowest Gini final, then it is root node.

Now, we have to decide what splitting value (40 or 50) we should put on the left side of Chest Pain.

![](/sources/DataMining-DecisionTree5.png) 

![](/sources/DataMining-DecisionTree5b.png)

Compute GINI final at splitting value = 40, given Yes to Chest pain

Compute GINI final at splitting value = 50, given Yes to Chest pain

Let's say we have extra candidate: Obese (with 2 levels), we also will compute GINI final of Obese as we did with Chest Pain

=> Choose splitting value with the lowest GINI final to do child node of left side of Chest Pain

Similarly, compute GINI final at splitting value = 40; 50 and Obese, given No to Chest pain

=> Choose splitting value with the lowest GINI final to do child node of right side of Chest Pain

**Example**: Compute GINI final at splitting value = 40 on the left side of Chest Pain. Now the left side of Chest Pain only has 3 patients in total. Among 3 these patients, there is 1 patient with weight < 40 and 2 people with weight > 40

![](/sources/DataMining-DecisionTree6.png)

GINI left
$$ 1 - (1)^2 - 0 = 1$$

GINI right
$$ 1 - (\frac{1}{2})^2 - (\frac{1}{2})^2 = 0.5 $$

GINI final
$$ \frac{1}{3} * 1 + \frac{2}{3} * 0.5 = 0.67 $$

**Example:** Compute Gini Final at spliting value = 50 on the left side of Chest Pain

![](/sources/DataMining-DecisionTree7.png)

GINI final
$$ 
     1 * (1 - (\frac{2}{3})^2 - (\frac{1}{3})^2) + 0 = 0.44 
$$

Let's say GINI final of spliting value = 50 is the lowest, given YES to Chest Pain, then the tree improves like this

![](/sources/DataMining-DecisionTree8.png)

**Step 5:** We keep spliting data into smaller until:
Reach min number of samples in a node

Gini impurity does not improve

Reach maximum depth allowed for tree

$$ I_G(D_\text{root}) = 1 - 2/5^2 + 2/5^2 + 1/5^2 = 0.64 $$

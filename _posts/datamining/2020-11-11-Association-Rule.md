---
layout: post
mathjax: true
title: "Association Rule - Market Basket Analysis - Part 1 "
read: 15
secondary: datamining
date: 2020-12-05
---
### 1. Affinity analysis (or Market basket analysis)

- Study of attributes or characteristics that go together
  
- Association rules take the form "If antecedent, then consequent"

![](/sources/association-rule1.png){:height="40%" width="40%"}

- Itemset is the list of all the items in the antecedent and the consequent. *k-itemset* is an itemset containing k items

- Implication here is co-occurrence and not causality

### 2. Metrics to measure association rule

**Case study**

- Total transactions in a supermarket on Sat is: 1,0000 transactions

- Consider: 
  
  -  1-itemsetA = {bread}
  
  -  1-itemsetB = {shampoo}
  
  - 2-itemsetC = {bread, milk}

  - 2-itemsetD = {shampoo, milk}

**SUPPORT** metric

The ratio of total transactions containing X and total transactions. Here, X can be 1-itemset or k-itemset.  

![](/sources/association-rule2.png){:height="50%" width="50%"}

SUPPORT of 2-itemsetC = {Total transactions containing bread and milk} / {Total transactions of supermarket on Sat} = 50/1,000 = 0.05

=> Itemset containing bread and milk occur 50 times out of a total of 1,000 transaction. If an itemset has very low **SUPPORT**, we do not enough information on the relationship between its item and so, no conclusions can be drawn from such a rule.

**CONFIDENCE** metric

For 2-itemsetC = {bread, milk}, check association from {bread} -> {milk}: Out of 100 customers bought bread, there was 80 customers bought milk. 

![](/sources/association-rule3.png){:height="50%" width="50%"}

For 2-itemsetD = {shampoo, milk}. {shampoo} -> {milk}: Out of 100 customers bought shampoo, there was 70 customers bought milk. Intuitively, it seems wrong because these two products have a week association. But confidence is still high. WHY? Because simply {milk} is a frequent itemset that presents in most of transactions.

*To avoid misleading about this high confidence value*, **LIFT** metric comes in to overcome this problem. 

**LIFT** metric

Case study

![](/sources/association-rule4.png){:height="40%" width="40%"}

Total transactions is 1,000. Out of 1,000 transactions, there are

  - 800 transactions containing milk (if containing only milk = 800 - 70 = 730)
  
  -  100 transactions containing shampoo (if containing only shampoo = 100 - 70 = 30)
  
  - There 70 transactions containing milk and shampoo. In another word, out of 100 transactions containing shampoo, there are 70 transactions containing additional milk. Similarly, out of 800 transactions containing milk, there are also 70 transactions containing additional shampoo.

=> Result: Confidence of {shampoo} -> {milk} = P(milk on shopping cart | shampoo) = 70 / 100 = 0.7

=> Now, to avoid misleading, we MUST consider: P(milk on shopping cart | WITHOUT shampoo) = 800 / 1,000 = 0.8

**Interpretation**

It turns out that without shampoo on the cart, P(milk on shopping cart) is 0.8. But if given shampoo on the cart, P(milk on shopping cart) reduces to 0.7. To measure exactly, we use LIFT = 0.7 / 0.8 = 0.87. LIFT value < 1 shows that having shampoo on the cart does not increase the chances of occurrence of milk on the cart in spite of the CONFIDENCE rule is high. 

![](/sources/association-rule5.png){:height="50%" width="50%"}

If LIFT > 1: there is a high association between {X} and {Y}: if customer has already bought X, there is a greater chances of buying Y.

### 3. Interpret association metrics in plain English

Example

Left handside: {squash} => Right handside: {beans}

- Support = 0.428: There are around 42.8% of customers purchased both squash and beans among total transactions

- Confidence = 0.857: Among those who purchased squash, there is around 85.7% of those who purchased beans

- Lift = 1.2: If we know customer purchases squash, there is 1.2 times more likely to buy beans than all of other customers.

### 4. Association rule

Next step is to generate rules from the entire list of items and identify the most important ones. This is not simple because supermarkets have thousands of different products and combination is such a pain.

How to come up with a set of most important association rules to be considered ? Using *Apriori algorithm*

Please read [Association Rule - Part 2](https://lytranp.github.io/notes/Association-Rule-2)

--------------------------
References

Anisha Garg, https://towardsdatascience.com/association-rules-2-aa9a77241654





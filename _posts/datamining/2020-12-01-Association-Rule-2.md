---
layout: post
mathjax: true
title: "Association Rule - Market Basket Analysis - Part 2 "
read: 15
secondary: datamining
date: 2020-12-05
---
Please read [Association Rule - Market Basket Analysis - Part 1](https://lytranp.github.io/notes/Association-Rule)

### 1. Why need Apriori algorithm ?

As we mentioned in the part 1, a supermarket has a thousands of products. If we have k attributes, we will have k*2^{k-1} possible association rules. E.g, if we have 10 products, we will have 10*2^9 = 5,120 rules. Therefore, we need this algorithm to reduce it to a more manageable size

There are 2 principal methods of representing this type of market basket data

- Use transactional data

![](/sources/association-rule-2-1.png){:height="40%" width="40%"}

- Use tabular data format 

![](/sources/association-rule-2-2.png){:height="40%" width="40%"}

This data is before applying Apriori algorithm.

### 2. Generate association rules using Apriori algorithm

Case study 

+ Transaction 1 (T1) contains items I1(bread), I2(milk), I5(shampoo)
  
+ Transaction 2 (T2) contains items I2(milk), I4(book)
  
+ Transaction 3 (T3) contains items I2(milk), I3(shoes) and so on

![](/sources/association-rule-2-3.png){:height="20%" width="20%"}

**Step 1**: k = 1

- Create a table counting occurrence of EVERY SINGLE items (1-itemset) in shopping cart (sup_count)

![](/sources/association-rule-2-4.png){:height="20%" width="20%"}

- Compare column sup_count (occurence) with ***minimum support*** (min_support: that was chosen based on experience and business). Assuming, if min_support = 2, we will remove items < min_support. As a result, we have a table as above, called itemsetA1 for the entire table.  

- Term: **Frequent itemsets** are the ones having support value >= ***minimum support*** (minimum threshold)

**Step 2**: k = 2

Choose frequent itemsets from step 1 (in another word, get itemsetA1) to generate itemsets of length 2 and count their occurences. 

![](/sources/association-rule-2-5.png){:height="20%" width="20%"}

Compare support count with ***minimum support*** (here, min_support = 2). Remove itemsets < min_support. As a result, we have this itemsetA2 (entire table)

![](/sources/association-rule-2-6.png){:height="20%" width="20%"}

**Step 3**: k = 3

Similar to above steps, using itemsetA2 to generate itemsets of length 3 and count their occurences. After that, compare with min_support. This give us itemsetA3

![](/sources/association-rule-2-7.png){:height="20%" width="20%"}

**Step 4**:

We stop here because no frequent itemsets are found further

### 2. Compute CONFIDENCE of each rule

Remember CONFIDENCE metric from [Association Rule - Market Basket Analysis - Part 1](https://lytranp.github.io/notes/Association-Rule)

![](/sources/association-rule3.png){:height="60%" width="60%"}

Example:

If rule {bread} -> {milk}, then Confidence = {Transactions containing both bread and milk} / {Transaction containing bread}

Similarly, in our above case study: 

+ If rule: {I1 , I2} -> {I3}
  
  => Confidence = {Transactions containing I1, I2, I3} / {Transaction containing I1, I2} = sup_count(I1, I2, I3) / sup_count(I1, I2) = 2 / 4 = 50%

+ If rule: {I1} -> {I2, I3}

  => Confidence = {Transactions containing I1, I2, I3} / {Transaction containing I1} = sup_count(I1, I2, I3) / sup_count(I1) = 2 / 6 = 33%

 ***Interpretation* for Confidence**

 A confidence 50% means that 50% of the customers who bought I1 and I2 also bought I3

 A confidence 33% means that 33% of the customers who bought I1 also bought I2 and I3

---------------------------------
**References**

https://www.geeksforgeeks.org/apriori-algorithm/?ref=lbp

https://www.analyticsvidhya.com/blog/2017/08/mining-frequent-items-using-apriori-algorithm/
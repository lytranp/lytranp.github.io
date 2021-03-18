---
layout: post
mathjax: true
title: "Stock Options"
read: 15
secondary: others
date: 2021-02-11
---


There are 2 types of options: puts (bet that a stock will fall) and calls (bet that a stock will rise)

1. Buy call - Sell call

- Assuming that the stock price yesterday is $10. Today, the stock price is $11. When stock seems to increase, a buyer guess that stock might continue increasing to at least $20 within 1 month.

- Seller is the person who have at least 100 stocks in hand (1 contract composes 100 stocks). Seller only can sell 1,2,3 (integer)...contract. 

=> So, there is a deal between seller and buyer: 

* Buyer: 

    - They want to buy the stock at cheap price when stock price increases in the future. 
    
    - So, they buy call and pay commission fee (or called cost of contract or premium) to seller so that if stock price increase over strike price $15, buyer will execute contract and buy stock from this seller with the price only at $15 whereas the stock's market price at that time is $20. 

    - For buyer to earn a profit: stock price would need to rise above the strike price AND cost of call on a contract

    - Buyer will lose entire premium if the stock price does not rise above the strike price + cost of call on a contract at the expiration date. 

    - Commission fee buyer has to pay depends on strike price and expiration date of contract. 

        + If current stock price is $11 and strike price is $12 and expiration date is long (4 month, 1 year...) 
        
        => Buyer is happy because there is a high chance that stock price will actually increase, and the buyer will be able to buy stock at cheap price.

        => Seller is sad because they have to sell at cheap price to this buyer whereas the market price is greater => Seller will sell call with high commission fee because there is high chance that buyer wins and execute the contract. 

* Seller: They want that the stock will not beyond strike price ($15), so they will not have to sell stocks to buyer at cheap price (strike price) when stock's market price at that time is $20, for example. And they simply received commission fee when selling call.

    -   When the stock price actually rises above strike price and buyer executes the contract, the seller can consider the following factors to see if they actually lost 

        + If the stock price at the time they bought was very low, for example 5$, then they still earn much profit because they received commission fee + sell stock at $15. If they had not sold the contract, they could sell the stock at market price $20, but certainly they would not have commission fee.

2. Buy put - Sell put

- Assuming that the current stock price is at $10 and it has tend to decrease. Buyer also believe that the stock price will continue decreasing to $5 in the future. So, they look for someone (seller) who believe that the stock price will increase to $15, then they will bet each other.

- To join in the game, buyer has to keep stocks at hands, seller has to deposit money to third platform (Robinhood) so that in the case contract executes, seller must re-buy stocks at the high price (strike price) from "put buyer".

- Buyer believes that the stock decreases and seller bets the stock price increase to $15 (strike price). If the buyer wins, seller has to purchase buyer's stocks at the price of $15, whereas the actual price at that time is only $7.

* Buyer: 

    - They buy put, and pay seller a premium.

    - If the stock actually decreases below the strike price ($15) in the future, they still can sell to "put seller" at the price of $15 whereas the market price at that time is only $7 

* Seller:

    - They got premium from seller.

    - If the stock price increases above strike price ($15), they get back the amount of money they deposited on 3rd party (Robinhood)

    - If the stock price decreases below strike price ($7), they still must re-purchase stocks from "put buyer" at the price of $15

    * Conclusion: as a seller, we accepts if and only if

        + We believe that the stock price will rise above strike price

        + Even when we must re-purchase stocks, we still believe that that is still good price

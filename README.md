# Market-Marker
Analytics FP interview Code Challenge
Problem 1
Backtesting

Problem 2
Initial Problem: 
Market-maker get paid for entering positions, but can not choose when to trade. Construct a strategy can make  a profit.

Assumption:
1. At each timestep market-marker is forcibly entered into a long position of size = S contracts with
probability p1 and independently a short position of size S with probability p2 (you may simultaneously get entered long and short, in which case your final additional position is 0). 
2. Market-marker gets $M per contract to be entered into the trades. Trading costs is $C per contract. Typically, C ＞ M.
3. Market-marker should maintain its open position smaller than L. .e., if S ＞ L then you may (and must) close at least [S – L] contracts immediately.

Ultimate Problem:
The initial problem can be interpreted into following problem: for what values of p1, p2, S, M, C, L would you expect to make money? even when M = 0, or even, M＜0?

Solution:
We can't decide when the opponents buy and sell, but we can decide to hedge or hold the open position. My method is generate our long & short signal (For the sake of simplicity, I pick Future B and use Moving Average to generate long & short signal).
If the opponents offer the trading we want to do (e.g. the opponent wants to sell and I want to buy), I will hold the opening position till my signal disappear. Other case, we simply hedging the opening position by simultaneously get entered long and short (e.g. the opponent wants to sell, so I buy it and sell it immediately).
We should also make sure our opening should smaller than the largest opening position L.

After back-tested my idea with python, it did make a profit on my dataset and I found out the some conditions that makes the strategies performs better when I tuned the parameters.
The trading size should be large enough. So the little profit we gain from the price difference can accumulate and cover the cost of fee. 
It seems that the larger p1 and p2 the better the performance.
Some parameters of my strategy can make money when M<=0. Performance can be imporve by making better signal to decide whether we should hedge or hold the open position (some advanced method better than Moving Average method I apply here).

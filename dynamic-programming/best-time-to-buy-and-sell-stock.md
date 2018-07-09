# Best Time to Buy and Sell Stock

Say you have an array for which the _i-\_th element is the price of a given stock on day \_i_.

If you were only permitted to complete at most one transaction \(i.e., buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Example 2:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

## Solution

We are looking for lowest price and then for the highest profit.

```
class Solution {
    public int maxProfit(int[] prices) {
        // take an element and calculate difference for all next elements (keep max only) repeate for other elements
        // O(n2)
        // int max = 0;
        // for (int i = 0; i < prices.length; i++) {
        //     for (int j = i + 1; j < prices.length; j++) {
        //         max = Math.max(max, prices[j] - prices[i]);
        //     }
        // }

        // O(n) [7,1,5,3,6,4]
        if (prices.length == 0) return 0;

        int min = prices[0];
        int maxProfit = 0;
        for (int i = 1; i < prices.length; i++) {
            min = Math.min(min, prices[i]);
            maxProfit = Math.max(maxProfit, prices[i] - min);
        }

        return maxProfit;
    }
}
```

Other solution to find the best price in only one pass.

```
public class Solution {
    public int maxProfit(int prices[]) {
        int minprice = Integer.MAX_VALUE;
        int maxprofit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minprice)
                minprice = prices[i];
            else if (prices[i] - minprice > maxprofit)
                maxprofit = prices[i] - minprice;
        }
        return maxprofit;
    }
}
```

Here is another alternative, probably more intuitive and simplier.

```
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) return 0;
        int minPrice = prices[0];
        int maxProfit = 0;
        for (int i = 1; i < prices.length; i++) {
            System.out.println("min: " + minPrice + ", max: " + maxProfit);
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else if (prices[i] - minPrice > maxProfit) {
                maxProfit = prices[i] - minPrice;
            }
        }
        return maxProfit;
    }
}
```

Here is the output.

```
min: 7, max: 0
min: 1, max: 0
min: 1, max: 4
min: 1, max: 4
min: 1, max: 5
```

More info from other [source](http://hanslen.me/2017/10/15/Best-Time-to-Buy-and-Sell-Stock-series-with-Dynamic-Programming-in-Java/). 


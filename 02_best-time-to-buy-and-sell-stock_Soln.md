https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/
https://neetcode.io/problems/buy-and-sell-crypto?list=neetcode150

121. Best Time to Buy and Sell Stock
Attempted
Easy
Topics
premium lock icon
Companies
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

 

Example 1:

Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
Example 2:

Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.

Pattern : Two Pointer and Sliding Window
**Brute in C#:**

    public class Solution {
        public int MaxProfit(int[] prices) {
            int max = 0;
            for(int j=0; j<=prices.Length-1; j++)
            {
                for(int i=j+1; i<=prices.Length-1; i++)
                {
                    int difference = prices[i] - prices[j];
                    if(difference > max)
                    {
                        max = difference;
                    }
                }
            }
            return max;
        }
    }

**Brute in Python**

    class Solution:
        def maxProfit(self, prices: List[int]) -> int:
            max = 0
            for i in range(len(prices)):
                for j in range(i+1,len(prices)):
                    difference = prices[j] - prices[i]
                    if(difference > max):
                        max = difference
            return max

**Better in C#**
    
    public class Solution {
        public int MaxProfit(int[] prices) {
            int max = 0;
            int left = 0;
            for(int right=1; right<=prices.Length-1; right++)
            {
                if(prices[right] > prices[left])
                {
                    int difference = prices[right] - prices[left];
                    if(difference > max)
                    {
                        max = difference;
                    }
                }
                else
                {
                    left = right;
                }
            }
            return max;
        }
    }

        
**Better in Python**

            class Solution:
        def maxProfit(self, prices: List[int]) -> int:
            left = 0;
            max = 0
            for right in range(1,len(prices)):
                if prices[right] > prices[left]:
                    difference = prices[right] - prices[left]
                    if(difference > max):
                        max = difference
                else:
                    left = right
            return max

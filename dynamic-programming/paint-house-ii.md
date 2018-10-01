# Paint House II

#### Description

There are a row of `n` houses, each house can be painted with one of the `k` colors. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a `n` x `k` cost matrix. For example, `costs[0][0]` is the cost of painting house `0` with color `0`; `costs[1][2]` is the cost of painting house `1` with color `2`, and so on... Find the minimum cost to paint all houses.

All costs are positive integers.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given `n` = 3, `k` = 3, `costs` = `[[14,2,11],[11,14,5],[14,3,10]]` return `10`

house 0 is color 2, house 1 is color 3, house 2 is color 2, `2 + 5 + 3 = 10`

#### Challenge

Could you solve it in O\(nk\)?



```java
public class Solution {
    /**
     * @param costs: n x k cost matrix
     * @return: an integer, the minimum cost to paint all houses
     */
    public int minCostII(int[][] costs) {
        // write your code here
        if(costs == null || costs.length == 0) 
        return 0;
        
        int n = costs.length;
        int m = costs[0].length;
        int[][] dp = new int[n][m];
        
        int last1 = Integer.MAX_VALUE;
        int last2 = Integer.MAX_VALUE;
        int last1y = -1;
        int last2y= -1;
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        int min1y = -1;
        int min2y = -1;
        for(int i = 0; i < m; i++)
            {
                dp[0][i] = costs[0][i];
                if(dp[0][i] == last1)
                    {
                        last2 = last1;
                        last2y = last1y;
                    }
                else if(dp[0][i] < last1)
                {
                    last2 = last1;
                    last1 = dp[0][i];
                    last2y = last1y;
                    last1y = i;
                    
                }else if(dp[0][i] < last2)
                    {
                        last2 = dp[0][i];
                        last2y = i;
                    }
                
            }
        
        
        
        
        
        for(int i = 1; i < n; i++)
        {
                for(int j = 0; j < m; j++)
            {
                if(j == last1y)
                    dp[i][j] = costs[i][j] + last2;
                else 
                    dp[i][j] = costs[i][j] + last1;
                if(dp[i][j] == min1)
                    {
                        min2 = min1;
                        min2y = min1y;
                    }
                else if(dp[i][j] < min1)
                    {
                        min2 = min1;
                        min1 = dp[i][j];
                        min2y = min1y;
                        min1y = j;
                    }
                else if(dp[i][j] < min2)
                    {
                        min2 = dp[i][j];
                        min2y = j;
                    }
                
            }
            last1 = min1;
            last2 = min2;
            last1y = min1y;
            last2y = min2y;
            min1 = Integer.MAX_VALUE;
            min2 = Integer.MAX_VALUE;
            min1y = -1;
            min2y = -1;
            
        }
        
        int res = Integer.MAX_VALUE;
        for(int j = 0; j < m; j++)
            if(dp[n-1][j] < res)
                res = dp[n-1][j];
        
        return res;        
            

    }
}
```


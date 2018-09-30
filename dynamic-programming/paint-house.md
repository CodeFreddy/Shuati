# Paint House

#### Description

There are a row of n houses, each house can be painted with one of the three colors: red, blue or green. The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a `n` x `3` cost matrix. For example, `costs[0][0]` is the cost of painting house `0` with color red; `costs[1][2]` is the cost of painting house `1` with color green, and so on... Find the minimum cost to paint all houses.

All costs are positive integers.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given `costs` = `[[14,2,11],[11,14,5],[14,3,10]]` return `10`

house 0 is blue, house 1 is green, house 2 is blue, `2 + 5 + 3 = 10`

```java
public class Solution {
    /**
     * @param costs: n x 3 cost matrix
     * @return: An integer, the minimum cost to paint all houses
     */
    public int minCost(int[][] costs) {
        // write your code here
        if(costs == null || costs.length == 0)
            return 0;
        int n = costs.length;
        int[][] dp = new int[n][3];
        
        for(int i = 0; i < 3; i++)
            dp[0][i] = costs[0][i];
        
        for(int i = 1; i < n; i++)
        {
            dp[i][0] = costs[i][0] + Math.min(dp[i-1][2], dp[i-1][1]);
            dp[i][1] = costs[i][1] + Math.min(dp[i-1][0], dp[i-1][2]);
            dp[i][2] = costs[i][2] + Math.min(dp[i-1][0], dp[i-1][1]);
            
        }
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < 3; i++)
            if(dp[n-1][i] < min)
                min = dp[n-1][i];
        return min;
    }
}
```




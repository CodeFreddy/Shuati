# Unique Paths



A robot is located at the top-left corner of a _m_ x _n_ grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

How many possible unique paths are there?

![](https://leetcode.com/static/images/problemset/robot_maze.png)  
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** _m_ and _n_ will be at most 100.

**Example 1:**

```text
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```text
Input: m = 7, n = 3
Output: 28
```

坐标类型dp

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[n][m];
        
        dp[0][0] = 1;
        for(int i = 1; i < n; i++)
            dp[i][0] = 1;
        for(int j = 1; j < m; j++)
            dp[0][j] = 1;
        for(int i = 1; i < n; i++)
            for(int j = 1; j < m; j++)
            {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        
        return dp[n-1][m-1];
    }
}
```


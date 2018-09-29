# Unique Paths II



A robot is located at the top-left corner of a _m_ x _n_ grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![](https://leetcode.com/static/images/problemset/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** _m_ and _n_ will be at most 100.

**Example 1:**

```text
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```



```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int n = obstacleGrid.length;
        int m = obstacleGrid[0].length;
        int[][] dp = new int[n][m];
        
        if(obstacleGrid[0][0] == 1) return 0;
        else
            dp[0][0] = 1;
        for(int i = 1; i < n; i++)
        {
            if(obstacleGrid[i][0] == 1)
                dp[i][0] = 0;
            else
                dp[i][0] = dp[i-1][0];
        }
        
        for(int j = 1; j < m; j++)
        {
            
            if(obstacleGrid[0][j] == 1)
                dp[0][j] = 0;
            else
                dp[0][j] = dp[0][j-1];
        }
        
        for(int i = 1; i < n; i++)
            for(int j = 1; j < m; j++)
            {
                if(obstacleGrid[i][j] == 1)
                    dp[i][j] = 0;
                else
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        return dp[n-1][m-1];
    }
}
```



一维数组

```java
public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    int width = obstacleGrid[0].length;
    int[] dp = new int[width];
    dp[0] = 1;
    for (int[] row : obstacleGrid) {
        for (int j = 0; j < width; j++) {
            if (row[j] == 1)
                dp[j] = 0;
            else if (j > 0)
                dp[j] += dp[j - 1];
        }
    }
    return dp[width - 1];
}
```


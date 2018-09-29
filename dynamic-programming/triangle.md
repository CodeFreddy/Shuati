# Triangle

#### Description

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.  


Bonus point if you are able to do this using only O\(n\) extra space, where n is the total number of rows in the triangle.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given the following triangle:

```text
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 \(i.e., 2 + 3 + 5 + 1 = 11\).



解法1： DFS， 遍历所有的结果 但是会超时。时间复杂度： O\(2^n\)， 因为x = 1, n = 1, x = 2, n = 2, x = 3,  n = 4 \(x 代表二维数组的层数\)。 

```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
     private int best = Integer.MAX_VALUE;
    public int minimumTotal(int[][] triangle) {
        // write your code here
        traverse(0,0,0, triangle);
        return best;
    }
    
    public void traverse(int x, int y, int sum, int[][] A)
    {
        if(x == A.length)
        {
            if(sum < best)
                best = sum;
            return;
        }
        
        traverse(x + 1, y, sum + A[x][y], A);
        traverse(x + 1, y+1, sum + A[x][y], A);
        
    }
}
```



解法2： divided conquer 和dfs一样 会超时

```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    public int minimumTotal(int[][] triangle) {
        // write your code here
        
        return dividedConquer(0, 0, triangle);
    }
    
    public int dividedConquer(int x, int y, int[][] A)
    {
        if(x == A.length)
        {
            return 0;
        }
        
        return A[x][y] + Math.min(dividedConquer(x + 1, y, A), dividedConquer(x + 1, y + 1, A));
    }
    
    
}
```



解法3： Divide Conquer and memorization

```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    
    public int minimumTotal(int[][] triangle) {
        // write your code here
        int n = triangle.length;
        int[][]h = new int[n][];
        for(int i = 0; i < n; i++)
            h[i] = new int[triangle[i].length];
        for(int i = 0; i < n; i++)
            Arrays.fill(h[i], Integer.MAX_VALUE);
        return memorization(0, 0, triangle, h);
    }
    
    public int memorization(int x, int y, int[][] A, int[][] h)
    {
        if(x == A.length)
        return 0;
        
        if(h[x][y] != Integer.MAX_VALUE)
        {
            return h[x][y];
        }
        
        h[x][y] = A[x][y] + Math.min(memorization(x+1,y, A, h), memorization(x + 1, y + 1, A, h));
        return h[x][y];
    }
    
    
}
```



解法4： 多重循环dp 自底向上

```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    public int minimumTotal(int[][] triangle) {
        // write your code here
        int n = triangle.length;
        int[][] A = new int[n][];
        for(int i = 0; i < n; i++)
            A[i] = new int[triangle[i].length];
            for(int j = 0; j < A[n - 1].length; j++)
            {
                A[n-1][j] = triangle[n - 1][j];
            }
            
      
      for(int i = n - 2; i >= 0; i--)
      for(int j = 0; j <= i; j++)
      {
          A[i][j] = Math.min(A[i + 1][j + 1], A[i + 1][j]) + triangle[i][j];
      }
        
        return A[0][0];
    }
}
```



解法5： 多重循环dp 自顶向下

```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers
     * @return: An integer, minimum path sum
     */
    public int minimumTotal(int[][] triangle) {
        // write your code here
        int n = triangle.length;
        int [][] A = new int[n][];
        for(int i = 0; i < n; i++)
            A[i] = new int[triangle[i].length];
        
        A[0][0] = triangle[0][0];
        
        for(int i = 1; i < n; i++)
            {
                A[i][0] = A[i - 1][0] + triangle[i][0];
                A[i][i] = A[i - 1][i - 1] + triangle[i][i];
            }
        
        for(int i = 1; i < n; i++)
        for(int j = 1; j < i; j++)
        {
            A[i][j] = Math.min(A[i-1][j-1], A[i-1][j]) + triangle[i][j];
        }
        
      int min = Integer.MAX_VALUE;
      for(int i = 0 ; i < triangle[n - 1].length; i++)
        if(A[n-1][i] < min)
            min = A[n-1][i];
    return min;    
    }
}
```


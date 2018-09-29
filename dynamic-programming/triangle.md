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



解法1： DFS， 遍历所有的结果 但是会超时。

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



解法2： divided conquer




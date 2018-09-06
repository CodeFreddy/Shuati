# N Queens

#### Description

The n-queens puzzle is the problem of placing n queens on an `n×n` chessboard such that no two queens attack each other.

Given an integer `n`, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.



N皇后问题， 每一行都必须要有一个皇后， 而皇后不能存在于同一列 同一行，或是对角线。

```text
经典的DFS递归回溯解法，大体思路就是对每一行，按每一列挨个去试，试到了就保存结果没试到就回溯。
难点大概就是用1个一维数组存皇后所在的坐标值。对于一个棋盘来说，每个点都有横纵坐标，用横纵坐标可以表示一个点。
而这道题巧就巧在，每一行只能有一个皇后，也就是说，对于一行只能有一个纵坐标值，所以用1维数组能提前帮助解决皇后不能在同一行的问题。
那么用一维数组表示的话，方法是：一维数组的下标表示横坐标（哪一行），而数组的值表示纵坐标（哪一列）。

例如：对于一个4皇后问题，声明一个长度为4的数组（因为行数为4）。
     A[] = [1,0,2,3]表达含义是：
     当前4个皇后所在坐标点为：[[0,1],[1,0],[2,2],[3,3]]（被我标蓝的正好是数组的下标，标粉的正好是数组的值）
     相当于：A[0] = 1, A[1] = 0, A[2] = 2, A[3] = 3 

这样以来，皇后所在的坐标值就能用一维数组表示了。
而正是这个一维数组，在回溯找结果的时候不需要进行remove重置操作了，因为回溯的话正好就回到上一行了，就可以再重新找下一个合法列坐标了。

因为是按照每一行去搜索的，当行坐标值等于行数时，说明棋盘上所有行都放好皇后了，这时就把有皇后的位置标为Q，没有的地方标为0。
按照上面讲的那个一维数组，我们就可以遍历整个棋盘，当坐标为（row，columnVal[row]）的时候，就说明这是皇后的位置，标Q就行了。
```

```java
public class Solution {
    /*
     * @param n: The number of queens
     * @return: All distinct solutions
     */
    public List<List<String>> solveNQueens(int n) {
        // write your code here
        List<List<String>> res = new ArrayList<>();
        if(n <= 0) return res;
        DFS(res, new int[n], 0, n);
        return res;
    }
    
    public void DFS(List<List<String>> res, int[] queens, int row, int n)
    {
        if(row == n)
        {
            List<String> unit = new ArrayList<>();
            for(int i = 0; i < n; i++)
            {
                StringBuilder str = new StringBuilder();
                
                for(int j = 0; j < n; j++)
                {
                    if(j == queens[i])
                        str.append("Q");
                    else
                        str.append(".");
                }
                unit.add(str.toString());
            }
            res.add(unit);
        }
        else{
            for(int i = 0; i < n; i++)
            {
                queens[row] = i;
                
                if(isValid(row, queens))
                {
                    DFS(res, queens, row+1, n);
                }
            }
        }
        
        
    }
    
    public boolean isValid(int row, int[] queens)
    {
        for(int i = 0; i < row; i++)
        {
            if(queens[row] == queens[i] || Math.abs(row - i)== Math.abs(queens[row] - queens[i]))
            return false;
            
        }
        return true;
    }
}
```


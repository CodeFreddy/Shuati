# Unique Binary Search Trees



Given _n_, how many structurally unique **BST's** \(binary search trees\) that store values 1 ... _n_?

**Example:**

```text
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

解题思路：

这道题是用动规来做， 因为可以看出 当前问题是和之前的问题相关的。比如 1个节点时 那么只可能会有一种情况， 建立一个数组，res\[n\] n表示节点个数。res\[0\] 设置为1， 没有节点那么也是一种情况。 res\[1\] = 1，res\[2\] = 2， 那么当n=3的时候， 会有以node 1为root， node 2 为root 和node 3 为root的情况

root 1： left: 0, right: 2 =&gt; f\(0\) \* f\(2\)

root 2: left: 1, right: 1 =&gt; f\(1\) \* f\(1\)

root 3: left: 2, right: 0 =&gt; f\(2\) \* f\(0\)

由此可以得出 f\(n\) = f\(0\) \* f\(n-1\) + f\(1\) \* f\(n - 2\) + ...+ f\(n-1\)\*f\(0\)

```java
class Solution {
    public int numTrees(int n) {
        int[] res = new int[n+1];
        res[0] = 1;
        for(int i = 2; i <= n; i++)
        {
            for(int j = 0; j < i; j++)
            {
                res[i] += res[j] * res[i-1 - j];
            }
        }
        return res[n];
    }
}
```




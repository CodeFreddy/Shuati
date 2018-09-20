# House Robber III



The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```text
Input: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

Output: 7 
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

**Example 2:**

```text
Input: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```

解题思路：

 dfs all the nodes of the tree, each node return two number, int\[\] num, num\[0\] is the max value while rob this node, num\[1\] is max value while not rob this value. Current node return value only depend on its children's value. Transform function should be very easy to understand.

如果要选取这个点抢劫， 那么left和right只能取数组位置1的值（也就是不能选做儿子和右儿子抢劫）。 那如果不选当前节点，那么最大值就是left的0和1最大值加上right的0和1最大值。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int rob(TreeNode root) {
        int[] num = new int[2];
        num = dfs(root);
        return Math.max(num[0], num[1]);
    }
    
    public int[] dfs(TreeNode cur)
    {
        if(cur == null) return new int[2];
        int[] left = dfs(cur.left);
        int[] right = dfs(cur.right);
        int[] res = new int[2];
        res[0] = left[1] + right[1] + cur.val;
        res[1] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        return res;
    }
}
```


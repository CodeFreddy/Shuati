# Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the depth of the two subtrees of _every_ node never differ by more than 1.

**Example 1:**

Given the following tree `[3,9,20,null,null,15,7]`:

```text
    3
   / \
  9  20
    /  \
   15   7
```

Return true.  
  
**Example 2:**

Given the following tree `[1,2,2,3,3,null,null,4,4]`:

```text
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

Return false.

递归解法： 对于每一个左节点和右节点都进行一次高度检查，如果发现存在不符合要求的高度差 直接返回-1。以此来避免不必要的重复操作

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
    public boolean isBalanced(TreeNode root) {
        if(height(root) == -1)
            return false;
        else 
            return true;
    }
    
    public int height(TreeNode root)
    {
        if(root == null) return 0;
        int lH = height(root.left);
        if(lH == -1)
            return -1;
        int rH = height(root.right);
        if(rH == -1)
            return -1;
        if(Math.abs(lH - rH) > 1)
            return -1;
        
        return Math.max(lH, rH) + 1;
        
    }
}
```


# Binary Tree Longest Consecutive Sequence

#### Description

Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child \(`cannot be the reverse`\).Have you met this question in a real interview?  YesProblem Correction

#### Example

For example,

```text
   1
    \
     3
    / \
   2   4
        \
         5
```

Longest consecutive sequence path is `3-4-5`, so return `3`.

```text
   2
    \
     3
    / 
   2    
  / 
 1
```

Longest consecutive sequence path is `2-3`,not`3-2-1`, so return `2`.

递归解法：

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of binary tree
     * @return: the length of the longest consecutive sequence path
     */
    public int longestConsecutive(TreeNode root) {
        // write your code here
        return helper(root, null, 0);
    }
    
    public int helper(TreeNode root, TreeNode parent, int curLen)
    {
        if(root == null) return 0;
        int length = 0;
        if(parent != null && parent.val + 1 == root.val)
        length = curLen + 1;
        else
            length = 1;
        int left = helper(root.left, root, length);
        int right = helper(root.right, root, length);
        return Math.max(length, Math.max(left, right));
    }
}
```


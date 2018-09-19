# Count Univalue Subtrees

#### Description

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given root = `{5,1,5,5,5,#,5}`, return `4`.

```text
              5
             / \
            1   5
           / \   \
          5   5   5
```

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
     * @param root: the given tree
     * @return: the number of uni-value subtrees.
     */
    private int count = 0;
    
    public int countUnivalSubtrees(TreeNode root) {
        // write your code here
        helper(root);
        return count;
    }
    
    public boolean helper(TreeNode root)
    {
        if(root == null) return true;
        boolean left = helper(root.left);
        boolean right = helper(root.right);
        if(left && right)
        {
            if(root.left != null && root.left.val != root.val)
            return false;
            if(root.right != null && root.right.val != root.val)
            return false;
            
            count++;
            return true;
        }
        return false;
    }
}
```


# Validate Binary Search Tree



Given a binary tree, determine if it is a valid binary search tree \(BST\).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.

**Example 1:**

```text
Input:
    2
   / \
  1   3
Output: true
```

**Example 2:**

```text
    5
   / \
  1   4
     / \
    3   6
Output: false
Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
             is 5 but its right child's value is 4.
```

解题思路：

参考：[https://leetcode.com/problems/validate-binary-search-tree/discuss/32112/Learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-\(Java-Solution\)](https://leetcode.com/problems/validate-binary-search-tree/discuss/32112/Learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-%28Java-Solution%29)

根据up主总结归纳的模板 可以利用迭代的dfs解决这一类的二叉树问题。 对于这道题需要理解的一点，如果一个二叉树合法， 那么用inorder的顺序从bottom up来获取节点， 左边的节点肯定小于它的父亲节点然后小于父节点的右边节点。也就是说左边的节点时最小的。

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
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        Stack<TreeNode> s = new Stack<>();
        TreeNode pre = null;
        while(root != null || !s.isEmpty())
        {
            while(root != null)
            {
                s.push(root);
                root = root.left;
                
            }
            
            root = s.pop();
            if(pre != null && root.val <= pre.val) return false;
            pre = root;
            root = root.right;
        }
        return true;
    }
}

```

递归dfs解法：

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
    public boolean isValidBST(TreeNode root) {
        return isValid(root, null, null);
    }
    
    public boolean isValid(TreeNode root, Integer min, Integer max)
    {
        if(root == null) return true;
        if(min != null && root.val <= min) return false;
        if(max != null && root.val >= max) return false;
        return isValid(root.left, min, root.val) && isValid(root.right, root.val, max);
    }
}
```


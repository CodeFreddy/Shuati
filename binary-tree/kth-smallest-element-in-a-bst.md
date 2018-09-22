# Kth Smallest Element in a BST

Given a binary search tree, write a function `kthSmallest` to find the **k**th smallest element in it.

**Note:**   
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Example 1:**

```text
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```

**Example 2:**

```text
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```

**Follow up:**  
What if the BST is modified \(insert/delete operations\) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

依然根据：[https://leetcode.com/problems/validate-binary-search-tree/discuss/32112/Learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-\(Java-Solution\)](https://leetcode.com/problems/validate-binary-search-tree/discuss/32112/Learn-one-iterative-inorder-traversal-apply-it-to-multiple-tree-questions-%28Java-Solution%29)

的思路 用迭代的dfs就可以完成：

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
    public int kthSmallest(TreeNode root, int k) {
        if(root == null) return 0;
        Stack<TreeNode> s = new Stack<>();
        while(root != null || !s.isEmpty())
        {
            while(root != null)
            {
                s.push(root);
                root = root.left;
            }
            
            root = s.pop();
            if(--k == 0) break;
            root = root.right;
        }
        return root.val;
    }
}
```

递归:

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
    private int number = 0;
    private int count = 0;
    
    public int kthSmallest(TreeNode root, int k) {
        if(root == null) return number;
        count = k;
        helper(root);
        return number;
    }
    
    public void helper(TreeNode root)
    {
        if(root == null) return;
        helper(root.left);
        count--;
        
        if(count == 0)
        {
            number = root.val;
            return;
        }
        
        helper(root.right);
    }
}
```


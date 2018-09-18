# Symmetric Tree

Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```text
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:  


```text
    1
   / \
  2   2
   \   \
   3    3
```

**Note:**  
Bonus points if you could solve it both recursively and iteratively.

递归解法：

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
    // recursion solution
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return helper(root.left, root.right);
    }
    
    public boolean helper(TreeNode left, TreeNode right)
    {
        if(left == null || right == null)
            return left == right;
        if(left.val != right.val)
            return false;
        return helper(left.left, right.right) && helper(left.right, right.left);
        
    }
}
```



迭代解法：

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
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        Stack<TreeNode> s = new Stack<>();
        TreeNode left, right;
        if(root.left != null)
        {
            if(root.right == null) return false;
            s.push(root.left);
            s.push(root.right);
        }else if(root.right != null)
            return false;
        
        while(!s.isEmpty())
        {
            if(s.size() % 2 != 0) return false;
            right = s.pop();
            left = s.pop();
            if(left.val != right.val) return false;
            if(left.left != null)
            {
                if(right.right == null) return false;
                s.push(left.left);
                s.push(right.right);
            }else if(right.right != null)
                return false;
            
            if(left.right != null)
            {
                if(right.left == null) return false;
                s.push(left.right);
                s.push(right.left);
            }else if(right.left != null)
                return false;
            
        }
        return true;
    }
}
```

